# Phần 1: Phân Tích Toàn Diện Tiến Độ và Sức Khỏe Dự Án

## 1.1 Tái Cấu Trúc Phạm Vi và Cơ Sở Kỹ Thuật Dự Án

Để đánh giá chính xác sức khỏe của dự án, phạm vi được thiết lập dựa trên các yêu cầu chức năng tiêu chuẩn cho một **"Smarthome Basic Kit"** sử dụng kiến trúc **ESP32**. Dự án đại diện cho một sáng kiến phát triển IoT cấp độ từ sơ cấp đến trung cấp, được thiết kế để kiểm soát các thiết bị điện áp cao và giám sát các điều kiện môi trường.

Việc xác định rõ phạm vi này là tiền đề cốt yếu để thực hiện các phân tích sai lệch sau này.

---

## 1.1.1 Phân Tích Danh Mục Vật Liệu Phần Cứng (BOM)

Nền tảng phần cứng được xác định là một ngăn xếp mô-đun tập trung vào **Espressif ESP32-WROOM-32**. Lựa chọn này được ưu tiên hơn so với ESP8266 nhờ khả năng xử lý lõi kép và ngăn xếp Wi‑Fi/Bluetooth tích hợp, mang lại hiệu suất vượt trội cho các ứng dụng đa luồng, đặc biệt là khi xử lý đồng thời các tác vụ mạng và điều khiển ngoại vi thời gian thực.

### Danh mục BOM

| Danh mục            | Thành phần               | Mô tả chi tiết      | Biện chứng kỹ thuật & vai trò hệ thống                                                                                 | Ước tính chi phí (USD) |
| ------------------- | ------------------------ | ------------------- | ---------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| Vi điều khiển (MCU) | ESP32 DevKit V1 (38-pin) | Bo phát triển ESP32 | GPIO dồi dào, Wi‑Fi/BLE tích hợp, xử lý lõi kép. Tách xử lý mạng (Core 0) và logic ứng dụng (Core 1) giúp giảm độ trễ. | $6.00 – $8.00          |
| Cơ chế kích hoạt    | Module Relay 4 kênh 5V   | Relay cách ly       | Active‑LOW, optocoupler PC817 bảo vệ logic 3.3V khỏi back‑EMF từ cuộn relay.                                           | $7.00 – $12.00         |
| Cảm biến môi trường | DHT11                    | Nhiệt độ/Độ ẩm      | Độ chính xác thấp (±2°C, ±5% RH), tốc độ 1Hz — điểm nghẽn cho tự động hóa chính xác.                                   | $1.00 – $3.00          |
| Quản lý năng lượng  | Hi‑Link HLK‑5M05 AC‑DC   | Nguồn AC‑DC         | Chuyển 220V AC sang 5V DC, dạng potted an toàn lắp âm tường.                                                           | $4.00 – $6.00          |
| Kết nối & tạo mẫu   | Jumper wire & Breadboard | Dây & bảng test     | Thuận tiện tạo mẫu nhanh nhưng độ tin cậy cơ học thấp, dễ lỗi chập chờn.                                               | ~$5.00                 |

**Tổng chi phí BOM (cấu hình cơ sở):** **~$23.00 – $34.00 / đơn vị**

---

## 1.1.2 Phạm Vi Chức Năng và Kiến Trúc Phần Mềm

Kiến trúc phần mềm dựa trên **Arduino Framework** hoặc **ESP‑IDF**, triển khai các chức năng cốt lõi sau:

1. **Giao diện máy chủ Web (Asynchronous Web Server)**
   Máy chủ web bất đồng bộ cung cấp dashboard điều khiển relay. Bắt buộc dùng thư viện bất đồng bộ (ví dụ: `ESPAsyncWebServer`) để tránh treo MCU khi có nhiều HTTP request.

2. **Đo lường từ xa qua MQTT (Telemetry)**
   Publish dữ liệu cảm biến lên broker (Mosquitto, HiveMQ). MQTT nhẹ, ổn định trong môi trường mạng kém.

3. **Cung cấp Wi‑Fi (Provisioning)**
   SmartConfig hoặc BLE provisioning để cấu hình mạng động, tránh hardcode — yếu tố phân biệt sản phẩm thực tế với dự án thử nghiệm.

4. **Logic tự động hóa cục bộ (Edge Logic)**
   Quy tắc cục bộ ("Nếu Nhiệt độ > 30°C thì bật Relay 1") giúp hệ thống hoạt động ngay cả khi mất kết nối mạng.

---

## 1.2 Đánh Giá Định Lượng Sức Khỏe Dự Án (EVM Analysis)

Giả định:

* **Thời gian kế hoạch:** 16 tuần (4 tháng)
* **Ngân sách:** $5,000 (tạo mẫu, nhân công kỹ thuật, sản xuất lô nhỏ)

### 1.2.1 Phân Tích Hiệu Suất Lịch Trình (Schedule Performance)

* **PV (Planned Value):** 75% tại Tuần 12 (hoàn tất PCB v1.0 và firmware ổn định).
* **EV (Earned Value):** 60% (web server hoạt động, MQTT & non‑blocking sensor chậm).

**SV (Schedule Variance):**

```
SV = EV - PV = 60% - 75% = -15%
```

→ Dự án chậm tiến độ đáng kể.

**SPI (Schedule Performance Index):**

```
SPI = EV / PV = 0.60 / 0.75 = 0.8
```

**Phân tích:** Mỗi giờ kế hoạch chỉ tạo ra ~48 phút giá trị thực tế, chủ yếu do vòng lặp gỡ lỗi phần cứng–phần mềm (nhiễu relay gây reset ESP32).

---

### 1.2.2 Phân Tích Hiệu Suất Chi Phí (Cost Performance)

* **AC (Actual Cost):** 80% ngân sách = $4,000 (re‑spin PCB, hao linh kiện khi stress test).

**CV (Cost Variance):**

```
CV = EV - AC = $3,000 - $4,000 = -$1,000
```

**CPI (Cost Performance Index):**

```
CPI = EV / AC = 0.6 / 0.8 = 0.75
```

**Phân tích:** Vượt ngân sách ~25% do đánh giá thấp chi phí tích hợp, đặc biệt là ổn định nguồn khi Wi‑Fi và relay kích hoạt đồng thời.

---

## 1.3 Dự Báo: EAC và ETC

### 1.3.1 EAC – Estimate at Completion

```
EAC = BAC / CPI = $5,000 / 0.75 = $6,666.67
```

→ Dự kiến vượt ngân sách **$1,667 (~33%)**.

### 1.3.2 ETC – Estimate to Complete

```
ETC = EAC - AC = $6,667 - $4,000 = $2,667
```

→ Cần bổ sung ngân sách hoặc cắt giảm phạm vi.

### 1.3.3 Dự Báo Thời Gian

```
Thời gian = 16 tuần / 0.8 = 20 tuần
```

→ Trễ **~4 tuần**, chủ yếu để ổn định firmware và xử lý edge‑case.

---

## 1.4 Phân Tích Nguyên Nhân Gốc Rễ Các Sai Lệch

### 1. Bất ổn giao diện phần cứng–phần mềm ("Ghost Trigger")

* **Vấn đề:** ESP32 reset khi điều khiển relay/tải cảm ứng.
* **Nguyên nhân:** Cách ly nguồn kém, sụt áp dưới ngưỡng brownout của ESP32.
* **Tác động:** Lãng phí thời gian debug phần mềm, giảm mạnh SPI.

### 2. Lỗi đọc cảm biến (NaN – DHT11)

* **Vấn đề:** Trả về NaN hoặc không đọc được.
* **Nguyên nhân:** Giao thức một dây nhạy timing, bị Wi‑Fi/FreeRTOS ngắt.
* **Tác động:** Phải bổ sung retry/interrupt handling, tăng thời gian phát triển.

### 3. Phức tạp trong Provisioning

* **Vấn đề:** Không thể hardcode Wi‑Fi, provisioning động phức tạp.
* **Nguyên nhân:** Thiếu thư viện chuẩn, cần quản lý state & handshake an toàn.
* **Tác động:** Bị đánh giá thấp trong WBS, gây trượt lịch giai đoạn tích hợp.
