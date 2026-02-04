# Phần 4: Kế Hoạch Phân Phối Sản Phẩm và Khung Bảo Trì Toàn Diện

## 4.1. Chiến Lược Phân Phối và Hậu Cần

Đối với **Smarthome Basic Kit**, chiến lược phân phối cần cân bằng giữa **an toàn vật lý** của linh kiện điện tử nhạy cảm và **trải nghiệm mở hộp (out-of-box experience)**, đặc biệt cho nhóm người dùng **DIY** và **sinh viên**.

### 4.1.1. Đóng Gói và Hậu Cần (Packaging & Logistics)

* **Bảo Vệ Tĩnh Điện (ESD Protection)**
  ESP32 và các mô-đun relay là thiết bị bán dẫn nhạy cảm với phóng điện tĩnh điện. **Tất cả linh kiện bán dẫn bắt buộc** phải được đóng gói trong **túi chống tĩnh điện (anti-static shielding bags)** nhằm giảm tỷ lệ **DOA (Dead on Arrival)**.

* **Phân Đoạn Bộ Kit**
  Các thành phần được chia thành các ngăn riêng biệt để tránh va đập và nhầm lẫn:

  * **Túi A – Bộ não:** Vi điều khiển chính (ESP32 DevKit).
  * **Túi B – Điện áp cao:** Giao diện điện áp cao (Relay, khối đầu cuối). Có **cảnh báo an toàn** rõ ràng.
  * **Túi C – Cảm biến & điện áp thấp:** Cảm biến (DHT11), dây jumper.

* **Tài Liệu Kèm Theo**
  Thẻ vật lý **Quick Start Guide** kèm **QR code** liên kết kho tài liệu số và video hướng dẫn. Cách này giảm chi phí in ấn và cho phép cập nhật nội dung mà **không cần thay đổi bao bì**.

### 4.1.2. Phân Phối Kỹ Thuật Số (Digital Distribution)

* **Kho Lưu Trữ Firmware (GitHub – Public)**
  Cấu trúc thư mục chuẩn hóa:

  ```text
  src/    # Mã nguồn theo module
  docs/   # Schematic, Fritzing, API docs
  bin/    # Firmware biên dịch sẵn (pre-compiled)
  tools/  # Script cấu hình & debug
  ```

  * Hỗ trợ nạp nhanh qua **ESP Flash Download Tool** cho người dùng không biên dịch mã nguồn.

---

## 4.2. Kế Hoạch Đào Tạo Người Dùng và Quy Trình Chuyển Giao

Mục tiêu là **giảm support ticket** và đảm bảo **tỷ lệ triển khai thành công cao**, đặc biệt với người dùng chuyển từ thiết bị **plug-and-play** sang **DIY kit**.

### 4.2.1. Giáo Trình Đào Tạo: *Zero to Automation*

#### Mô-đun 1: Cơ Bản Phần Cứng & An Toàn Điện (45 phút)

* **Mục tiêu:** Hiểu kết nối vật lý và rủi ro an toàn.
* **Nội dung:**

  * **An toàn điện:** Lý thuyết 220V/110V; khuyến nghị thực hành với tải 12V để an toàn.
  * **Logic chân cắm:** VIN vs 3V3 vs GPIO; relay 5V phải cấp từ **VIN**.
  * **Thực hành đấu nối:** Lắp mạch trên breadboard theo sơ đồ Fritzing; tránh tiếp xúc lỏng.

#### Mô-đun 2: Cấu Hình & Cung Cấp Mạng (30 phút)

* **Mục tiêu:** Kết nối Wi-Fi cục bộ.
* **Nội dung:**

  * **AP Mode:** Nhận biết Wi-Fi `Smarthome-Setup`.
  * **Captive Portal:** Nhập thông tin Wi-Fi qua trình duyệt, không hardcode.
  * **Xác minh:** IP, RSSI qua Serial Monitor hoặc LED trạng thái.

#### Mô-đun 3: Bảng Điều Khiển & Tự Động Hóa (45 phút)

* **Mục tiêu:** Vận hành và thiết lập logic.
* **Nội dung:**

  * **Giao diện Web:** Bật/tắt relay, xem biểu đồ cảm biến (giải thích độ trễ).
  * **Quy tắc tự động:** Ví dụ *Relay 1 ON nếu T > 28°C*; áp dụng **Hysteresis**.
  * **Tích hợp di động:** MQTT với **Blynk** hoặc **Home Assistant**.

### 4.2.2. Danh Sách Kiểm Tra Chuyển Giao (Handover Checklist)

| Hạng mục  | Mục kiểm tra       | Tiêu chí xác nhận                          |
| --------- | ------------------ | ------------------------------------------ |
| Vật lý    | Dây dẫn            | Không lỏng; terminal relay siết **0.5 Nm** |
| Vật lý    | Vị trí cảm biến    | DHT11 không gần nguồn nhiệt                |
| Mạng      | Cường độ tín hiệu  | RSSI **> -70 dBm**                         |
| Bảo mật   | Thông tin xác thực | Đã đổi mật khẩu mặc định `admin`           |
| Chức năng | Trạng thái relay   | Chuyển mạch dứt khoát, không reset ESP32   |
| Chức năng | Dữ liệu cảm biến   | Cập nhật 10s, sai số trong giới hạn        |
| Phục hồi  | Chu kỳ nguồn       | Tự kết nối Wi-Fi lại < **60s**             |

---

## 4.3. Kế Hoạch Bảo Trì & Cam Kết Mức Độ Dịch Vụ (SLA)

Bảo trì IoT cần xem xét **lão hóa phần cứng** và **biến động mạng**.

### 4.3.1. Thỏa Thuận Mức Độ Dịch Vụ (SLA – Giả định)

#### 1) Phạm vi dịch vụ

* MQTT Broker (nếu có), firmware thiết bị (trừ mất điện lưới), và hỗ trợ kỹ thuật.

#### 2) Mục tiêu khả dụng (Availability)

* **Kết nối đám mây:** **99.9%/tháng** (downtime ≤ **43.2 phút/tháng**).
* **Độ ổn định thiết bị:** Không reboot tự phát quá **1 lần/72 giờ**.

#### 3) Cấp độ hỗ trợ & thời gian phản hồi

| Mức độ | Mô tả                               | Phản hồi | Giải quyết        |
| ------ | ----------------------------------- | -------- | ----------------- |
| Sev 1  | Lỗi toàn hệ thống / nguy cơ an toàn | < 4 giờ  | < 24 giờ          |
| Sev 2  | Lỗi chức năng chính                 | < 24 giờ | < 3 ngày làm việc |
| Sev 3  | Lỗi nhỏ / thẩm mỹ                   | < 3 ngày | Bản vá kế tiếp    |

#### 4) Tín dụng dịch vụ

* Khả dụng < **99.0%** → **10%** tín dụng tháng đó hoặc **1 tháng hỗ trợ cao cấp**.

### 4.3.2. Quy Trình Bảo Trì Định Kỳ

#### Bảo trì hàng quý

1. **Hiệu chuẩn cảm biến:** Drift > **2°C** → bù **offset** trong phần mềm.
2. **Siết khối đầu cuối:** Tránh hồ quang điện do chu kỳ nhiệt.
3. **Đánh giá log:** Tìm cảnh báo **Brownout**, **Heap leak**.

#### Chiến lược cập nhật Firmware (OTA)

1. **Cơ chế:** AsyncElegantOTA hoặc HTTP Update (ESP32).
2. **Chống brick (Rollback):** Xác minh **hash**, tự động quay về phân vùng ổn định nếu lỗi.
3. **Lịch trình:** Đẩy cập nhật giờ thấp điểm (ví dụ **03:00**).
