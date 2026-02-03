# BÁO CÁO ĐÁNH GIÁ KẾT QUẢ DỰ ÁN (MÔ PHỎNG)
**Dự án:** Phát triển Hệ thống "SmartHome Basic Kit"

---

## 1. Tổng quan Hiệu quả Dự án (Executive Summary)

Dự án đã chính thức khép lại sau 9 tuần triển khai chính thức + 1 tuần xử lý phát sinh. Mặc dù đối mặt với thách thức lớn về tích hợp hệ thống, nhóm đã hoàn thiện sản phẩm với đầy đủ tính năng cam kết.

* **Trạng thái cuối cùng:** Đã hoàn thành (Completed).
* **Mức độ thành công:** Đạt yêu cầu kỹ thuật, trễ hạn nhẹ và vượt ngân sách trong biên độ cho phép.
* **Đánh giá chung:** Minh chứng cho hiệu quả của mô hình lai (**Hybrid**), nhưng cũng bộc lộ lỗ hổng trong quản lý giao tiếp nội bộ.

---

## 2. Bảng đối chiếu các chỉ số mục tiêu (Baseline vs. Actual)

| Chỉ số (KPIs) | Kế hoạch (Baseline) | Thực tế (Actual) | Chênh lệch (Variance) |
| :--- | :--- | :--- | :--- |
| **Thời gian** | 9 tuần | 10 tuần | +1 tuần (Trễ 11%) |
| **Ngân sách** | 52.000.000 VNĐ | 54.800.000 VNĐ | +2.800.000 VNĐ (Vượt 5.3%) |
| **Tính năng** | 100% Scope | 100% Scope | Hoàn thành đầy đủ |
| **Chất lượng** | Latency < 300ms | Latency ~ 200ms | Vượt mong đợi |

---

## 3. Phân tích chi tiết sự cố điểm nhấn (Highlight Incident)

### Sự cố: Lỗi "Handshake" giữa App và Hub (Tuần 7)



**Phân tích nguyên nhân (Root Cause Analysis):**
* **Con người:** Đội App và đội Firmware thiếu buổi họp đồng bộ (Sync-up meeting) khi thay đổi API.
* **Quy trình:** Mô hình Agile của đội App thay đổi cấu trúc JSON liên tục nhưng mô hình Waterfall của đội Hardware không cập nhật kịp tài liệu thiết kế.
* **Công cụ:** Thiếu môi trường giả lập (Mock Server) đủ tốt để đội App test trước khi có mạch thật.

**Khắc phục:** Nhóm đã dành trọn Tuần 8 để chuẩn hóa lại giao thức và mua bổ sung thiết bị đo kiểm logic nhằm xác định chính xác lỗi nằm ở tầng vật lý hay tầng ứng dụng.

---

## 4. Bài học kinh nghiệm (Lessons Learned)

### Bài học 1: Quản lý sự phụ thuộc trong mô hình Hybrid
Trong các dự án IoT, cần thiết lập **"Interface Contract"** (Hợp đồng giao diện) chặt chẽ. Mọi thay đổi về Data Packet trên App phải được ký duyệt và cập nhật vào tài liệu chung (Swagger/Postman) ngay lập tức.

### Bài học 2: Chiến lược "Tích hợp sớm" (Early Integration)
Không đợi đến khi có mạch in hoàn chỉnh (Final PCB) mới bắt đầu test kết nối. Nên thực hiện kiểm thử trên các bo mạch phát triển (Development Boards) ngay từ tuần 4 để phát hiện xung đột giao thức sớm hơn.

### Bài học 3: Quản lý dự phòng ngân sách (Contingency)
Dự án kỹ thuật/R&D luôn tiềm ẩn rủi ro hỏng hóc linh kiện hoặc cần thiết bị đo kiểm phát sinh. Việc dành ra **10% dự phòng phí** là quyết định đúng đắn giúp nhóm xử lý sự cố Tuần 7 mà không bị gián đoạn tài chính.

---

## 5. Kết luận

Nhìn chung, dự án **SmartHome Basic Kit** đã đạt được mục tiêu cốt lõi là tạo ra sản phẩm chạy được. Sự cố kết nối là một bài học đắt giá giúp thành viên nhóm hiểu rằng: trong dự án công nghệ, **Giao tiếp (Communication)** quan trọng tương đương với **Kỹ thuật (Technical)**.