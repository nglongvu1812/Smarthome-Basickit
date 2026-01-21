# Báo cáo Nghiên cứu và Kế hoạch Chiến lược  
## Tái cấu trúc Dự án SmartHome Basic Kit – Giai đoạn Pilot Run  
*(Giai đoạn sản xuất thử nghiệm)*

---

## 1. Tái định nghĩa Phạm vi và Mục tiêu Dự án  
### (Scope Redefinition)

Việc nâng cấp dự án lên quy mô **Pilot Run** đòi hỏi sự thay đổi triệt để trong **Cấu trúc Phân chia Công việc (WBS)** và các tiêu chí nghiệm thu.  
Phạm vi dự án không còn giới hạn ở việc *“làm cho mạch chạy được”* mà mở rộng sang *“làm cho 50 mạch chạy giống hệt nhau và ổn định”*.

---

### 1.1. Chuyển dịch từ Prototyping sang Pilot Run (EVT / DVT)

Trong giai đoạn trước, dự án hoạt động ở mức **Kiểm thử Xác thực Kỹ thuật (EVT – Engineering Validation Test)**, nơi mục tiêu chính là chứng minh các chức năng cơ bản như bật/tắt đèn qua App hoạt động.

Tuy nhiên, với **ngân sách 55 triệu VNĐ cho 50 bộ**, dự án chính thức bước vào giai đoạn:

- **DVT – Design Validation Test**
- Chuẩn bị cho **PVT – Production Validation Test**

#### Các thay đổi cụ thể trong phạm vi:

**• Phần cứng (Hardware)**  
- Chuyển từ PCB đơn lẻ (hàn tay) sang **PCB dạng Panel (Panelized PCB)**  
- Tích hợp **Fiducial Mark** phục vụ máy gắp linh kiện tự động (Pick & Place)  
- Tuân thủ nghiêm ngặt **DFM – Design for Manufacturing** để giảm lỗi SMT  

**• Cơ khí (Mechanical)**  
- Thay thế hộp nhựa khoét tay bằng **vỏ hộp thiết kế tùy chỉnh (Custom Enclosure)**  
- Thiết kế bằng CAD, tối ưu cho **in 3D SLA Resin**  
- Bề mặt mịn, tiệm cận sản phẩm đúc nhựa

**• Firmware & Software**  
- Mở rộng phạm vi sang **Flash & Test tại nhà máy**
- Firmware tích hợp **Factory Test Mode**
- Test nhanh GPIO, Wi-Fi, Relay trong **< 30 giây / thiết bị**
- Không cần pairing App người dùng

---

### 1.2. Cập nhật Cấu trúc Phân chia Công việc (WBS)

WBS cũ tập trung vào thiết kế và lập trình.  
WBS mới tăng mạnh tỷ trọng **Vendor Management** và **Quality Control (QC)**.

#### WBS Cấp 1 (Mở rộng):

1. **Quản trị Dự án**  
   - Quản lý ngân sách 55 triệu  
   - Quản lý rủi ro thuê ngoài  

2. **R&D Phần cứng (DFM)**  
   - Thiết kế lại PCB cho SMT  
   - Tối ưu hóa BOM  

3. **R&D Cơ khí**  
   - Thiết kế vỏ hộp  
   - In mẫu thử  
   - Tối ưu độ dày Resin  

4. **Chuỗi cung ứng & Mua sắm**  
   - Tìm nguồn linh kiện giá sỉ  
   - Đàm phán PCB / SMT  

5. **Sản xuất & Gia công (Outsourcing)**  
   - Giám sát SMT  
   - In 3D hàng loạt  

6. **Lắp ráp & Hoàn thiện (In-house)**  
   - Lắp PCB vào vỏ  
   - Đóng gói  

7. **Kiểm soát Chất lượng (QA / QC)**  
   - IQC (linh kiện đầu vào)  
   - OQC (thành phẩm)  

8. **Phát triển Phần mềm**  
   - App người dùng  
   - Tool test sản xuất  

---

## 2. Chiến lược Chuỗi cung ứng và Tối ưu hóa BOM  
*(Bill of Materials)*

Với ngân sách **55 triệu VNĐ cho 50 bộ (~1.1 triệu/bộ)** bao gồm cả phát triển, nhân sự và rủi ro, **tối ưu BOM là yếu tố sống còn**.

Dữ liệu giá dựa trên thị trường Việt Nam **2024–2025**.

---

### 2.1. Phân tích và Lựa chọn Linh kiện Chính

#### 2.1.1. Vi điều khiển (MCU): ESP32-WROOM-32

**Lý do chọn**
- Hiệu năng/giá thành tốt  
- Wi-Fi + Bluetooth  
- Cộng đồng lớn, giảm rủi ro firmware  

**Chiến lược mua**
- Giá lẻ: ~120.000 VNĐ  
- Giá sỉ (50+): 65.000 – 85.000 VNĐ  

**Tác động tài chính**
- 55 module × 70.000 = **3.850.000 VNĐ**
- Tiết kiệm ~ **2.7 triệu VNĐ (~40%)**

---

#### 2.1.2. Khối Nguồn: Hi-Link HLK-5M05 (5V/5W)

**Yêu cầu**
- An toàn điện 220V  
- Cách ly, độ bền công nghiệp  

**Giải pháp**
- Module nguồn đúc kín HLK-5M05

**Chi phí**
- Giá sỉ: ~54.000 VNĐ  
- 55 cái → **2.970.000 VNĐ**

---

#### 2.1.3. Khối Chấp hành (Relay & Dimmer AC)

**Relay**
- Dùng relay rời (SRD-05VDC-SL-C) + Optocoupler (PC817)
- Giá linh kiện rời: **5.000 – 7.000 VNĐ**

**Dimmer AC**
- Tự thiết kế: Triac BTA16 + Zero-cross (H11AA1)
- Rủi ro nhiễu & nhiệt cao

**Phương án Pilot Run**
- Dùng module Dimmer AC RobotDyn  
- Giá: 25.000 – 40.000 VNĐ  
- Hoặc tích hợp PCB: ~15.000 VNĐ/BOM

---

### 2.2. Chiến lược Quản lý Rủi ro Mua sắm

- **Đa dạng hóa nguồn cung**
  - Không phụ thuộc 1 nhà cung cấp
- **Buffer Stock**
  - +10% linh kiện thụ động  
  - +5% linh kiện giá cao (MCU, Nguồn)

---

## 3. Chiến lược Thuê ngoài (Outsourcing Strategy)

### 3.1. Gia công PCB & PCBA

**Chi phí dự kiến**
- Setup SMT: 400.000 – 1.000.000 VNĐ
- Hàn SMT: 100 – 300 VNĐ/pad  
- PCB 2 lớp (10×10cm): 25.000 – 30.000 VNĐ  

**Tổng PCBA**
- **100.000 – 150.000 VNĐ / board**

---

### 3.2. Gia công Vỏ hộp – In 3D SLA Resin

**Vật liệu**
- Resin ABS-like hoặc High Temp

**Chi phí**
- 3.500 – 5.000 VNĐ/gram

**Tối ưu thiết kế**
- Wall thickness: 1.5 – 2mm  
- Trọng lượng: 40 – 50g  
- Chi phí: **150.000 – 200.000 VNĐ / vỏ**

---

## 4. Phân tích Tài chính và Phân bổ Ngân sách

### Bảng 1: Dự toán Ngân sách Chi tiết cho 50 Bộ

| Hạng mục | Thành tiền (VNĐ) |
|--------|------------------|
| Vật tư Linh kiện (BOM) | 15.950.000 |
| Gia công (Outsourcing) | 14.500.000 |
| Nhân sự & Phát triển | 18.000.000 |
| Công cụ & Thiết bị | 4.000.000 |
| Dự phòng rủi ro (~5%) | 2.550.000 |
| **TỔNG CỘNG** | **55.000.000** |

---

### Phân tích tổng quan

- **Chi phí phần cứng + gia công ≈ 55%** → hợp lý cho dự án phần cứng
- **Vỏ hộp (10 triệu)** là hạng mục lớn nhất → có thể cắt giảm bằng:
  - FDM cho đáy
  - SLA cho mặt trước
- **Ngân sách nhân sự (18 triệu)** giúp giảm rủi ro sai thiết kế hàng loạt

---

**Kết luận:**  
Kế hoạch Pilot Run được thiết kế theo tư duy sản xuất thực tế, cân bằng giữa chi phí – chất lượng – rủi ro, tạo nền tảng vững chắc để tiến tới PVT và thương mại hóa.
