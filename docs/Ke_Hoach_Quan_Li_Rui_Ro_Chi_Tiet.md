# Kế hoạch Quản lý Rủi ro Chi tiết (Risk Register)

Trong mô hình **Outsourcing** và **Pilot Run**, rủi ro chuyển dịch từ nhóm **kỹ thuật nội bộ** sang **đối tác bên ngoài** và **chuỗi cung ứng**. Dưới đây là **Sổ theo dõi Rủi ro (Risk Register)** được cập nhật cho dự án.

---

## Bảng 2. Sổ theo dõi Rủi ro (Risk Register)

| Mã      | Mô tả Rủi ro (Risk Description)                                                                  | Phân loại            | Tác động (1-5)   | Khả năng (1-5) | Mức độ (Risk Score) | Chiến lược Ứng phó (Mitigation Plan)                                                                                                                                  | Người chịu trách nhiệm |
| ------- | ------------------------------------------------------------------------------------------------ | -------------------- | ---------------- | -------------- | ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| **R01** | Thiếu hụt linh kiện chính (ESP32 / IC nguồn) do thị trường khan hiếm hoặc nhà cung cấp chậm giao | Chuỗi cung ứng       | 5 (Nghiêm trọng) | 3 (Trung bình) | **15 (Cao)**        | - Mua stock ngay khi chốt thiết kế, không đợi sát ngày sản xuất<br>- Xác định ít nhất 2 nhà cung cấp thay thế (ví dụ: Hshop, DigiKey)                                 | Trưởng nhóm Mua sắm    |
| **R02** | Lỗi thiết kế PCB hàng loạt (sai footprint, sai sơ đồ) phát hiện sau khi đã gia công 50 mạch      | Kỹ thuật / Tài chính | 5 (Thảm họa)     | 2 (Thấp)       | **10 (Cao)**        | - Bắt buộc làm 5 mạch mẫu (Golden Sample) và test kỹ trước khi ký lệnh sản xuất<br>- Thuê freelancer chuyên nghiệp review mạch in                                     | Trưởng nhóm Phần cứng  |
| **R03** | Chất lượng gia công SMT kém (hàn nguội, lệch linh kiện, thiếu thiếc)                             | Chất lượng           | 3 (Trung bình)   | 3 (Trung bình) | **9 (Cao)**         | - Chọn đối tác gia công uy tín có bảo hành rework<br>- Quy định rõ tiêu chuẩn chấp nhận (Acceptance Criteria) trong hợp đồng<br>- Thực hiện test chức năng 100% (OQC) | Trưởng nhóm QC         |
| **R04** | Vỏ hộp in 3D bị cong vênh do nhiệt từ mạch điện hoặc co ngót vật liệu                            | Kỹ thuật             | 3 (Trung bình)   | 4 (Cao)        | **12 (Cao)**        | - Sử dụng nhựa High-Temp Resin<br>- Thiết kế khe tản nhiệt trên vỏ<br>- Test nhiệt độ hoạt động liên tục 24 giờ trên mẫu thử                                          | Trưởng nhóm Cơ khí     |
| **R05** | Freelancer chậm tiến độ hoặc không bàn giao đúng chất lượng cam kết                              | Nhân sự              | 4 (Cao)          | 2 (Thấp)       | **8 (Trung bình)**  | - Chia nhỏ thanh toán theo từng mốc (Milestone-based payment)<br>- Yêu cầu bàn giao file thiết kế định kỳ hàng tuần                                                   | Quản lý Dự án (PM)     |
| **R06** | Firmware không ổn định (treo, mất kết nối) khi vận hành số lượng lớn                             | Kỹ thuật             | 3 (Trung bình)   | 3 (Trung bình) | **9 (Cao)**         | - Tích hợp Watchdog Timer<br>- Bắt buộc có OTA Update để vá lỗi từ xa mà không cần thu hồi thiết bị                                                                   | Trưởng nhóm Firmware   |

---

## 7. Quy trình Kiểm soát Chất lượng (QC Protocols)

Để đảm bảo lô **Pilot 50 sản phẩm** đạt chuẩn, quy trình QC được xây dựng theo mô hình công nghiệp **IQC – PQC – OQC**.

### 7.1. Kiểm soát Chất lượng Đầu vào (IQC – Incoming Quality Control)

* **PCB**
  Kiểm tra ngoại quan mạch in trần: màu sắc, độ phủ sơn chống hàn, mạ pad.
  Đảm bảo không đứt mạch, không chập via.

* **Linh kiện**
  Kiểm tra mã linh kiện (Part Number) trên cuộn/khay so với BOM.
  Đo ngẫu nhiên giá trị điện trở, tụ điện bằng LCR Meter.

### 7.2. Kiểm soát Chất lượng Quá trình (PQC – Process Quality Control)

* **Giám sát SMT**
  Nếu có thể, cử người giám sát trực tiếp tại xưởng SMT trong ngày chạy máy để xử lý ngay lỗi phát sinh (ví dụ: lỗi feeder, linh kiện không được gắp).

* **First Article Inspection (FAI)**
  Yêu cầu đơn vị gia công hàn trước **1 mạch đầu tiên**, kiểm tra kỹ dưới kính hiển vi và test chức năng.
  Chỉ khi đạt yêu cầu mới cho phép chạy tiếp 49 mạch còn lại.

### 7.3. Kiểm soát Chất lượng Đầu ra (OQC – Outgoing Quality Control)

* **Xây dựng Jig Test**
  Với số lượng 50 mạch, không thể test thủ công.
  Cần chế tạo **Test Jig** sử dụng kim lò xo (Pogo Pins) tiếp xúc vào các Test Point trên PCB.

* **Quy trình Test**

  1. Cấp nguồn → kiểm tra dòng tiêu thụ (quá dòng thì ngắt ngay).
  2. Nạp firmware test tự động.
  3. Mạch tự động bật/tắt relay, nháy LED, gửi gói tin Wi-Fi.
  4. Phần mềm trên máy tính ghi nhận kết quả **PASS / FAIL**.

* **Burn-in Test**
  Chọn ngẫu nhiên **5–10% sản phẩm (khoảng 5 thiết bị)** để chạy liên tục 48 giờ ở tải tối đa nhằm loại bỏ lỗi sớm (Infant Mortality).

---

## 8. Kế hoạch Hành động Tuần 8–9 (Recovery Plan)

Để đưa chỉ số **SPI từ 0.77 về mức an toàn (> 0.9)**, nhóm dự án cần thực hiện các hành động khẩn cấp sau:

1. **Phê duyệt mẫu (Approval)**
   Tech Lead phải chốt file thiết kế PCB bản sửa lỗi (**Rev 1.1**) trong vòng **24 giờ**.

2. **Đặt hàng nhanh (Fast-track)**
   PM thực hiện thanh toán ngay **50% tiền cọc** cho xưởng SMT và chọn gói dịch vụ **Express**, chấp nhận giảm quỹ dự phòng để đổi lấy thời gian.

3. **Chuẩn bị song song**
   Trong khi chờ mạch về (khoảng 7 ngày):

   * Hoàn tất in 3D **50 vỏ hộp**
   * Chuẩn bị sẵn ốc vít, dây nối
   * Đội QC hoàn thiện **Jig Test** để có thể test ngay khi mạch được giao

---

*Hết tài liệu*
