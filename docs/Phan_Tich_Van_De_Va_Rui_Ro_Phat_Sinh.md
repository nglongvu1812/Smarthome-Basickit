```md
# I. Phân tích Vấn đề của Dự án

## 1. Vấn đề tổng thể của đề tài

Dự án **SmartHome Basic Kit** không chỉ là một hệ thống phần mềm đơn thuần mà là một hệ thống tích hợp gồm nhiều thành phần khác nhau, bao gồm:
- Thiết bị phần cứng IoT
- Hệ thống phần mềm điều khiển
- Hạ tầng mạng và Internet
- Người dùng cuối với trình độ công nghệ khác nhau

Sự kết hợp này làm phát sinh nhiều vấn đề phức tạp hơn so với các dự án web hoặc ứng dụng thông thường. Chỉ cần một thành phần trong hệ thống gặp sự cố cũng có thể ảnh hưởng đến toàn bộ hoạt động của hệ thống SmartHome.

---

## 2. Vấn đề về nghiệp vụ và nhu cầu người dùng

### 2.1. Vấn đề từ phía người dùng

Người dùng mục tiêu của **SmartHome Basic Kit** chủ yếu là các hộ gia đình phổ thông, không có kiến thức chuyên sâu về công nghệ. Tuy nhiên, hệ thống SmartHome lại yêu cầu người dùng thực hiện nhiều thao tác mang tính kỹ thuật như:
- Kết nối Wi-Fi
- Cấu hình thiết bị
- Quản lý tài khoản và phân quyền sử dụng

Điều này tạo ra mâu thuẫn giữa:
- Mong muốn hệ thống **đơn giản, dễ sử dụng**
- Thực tế hệ thống có **độ phức tạp kỹ thuật cao**

Nếu không được giải quyết hợp lý, người dùng có thể:
- Cài đặt sai thiết bị
- Hiểu sai trạng thái hoạt động của hệ thống
- Mất niềm tin vào sản phẩm

---

### 2.2. Vấn đề từ phía dự án / đơn vị phát triển

Từ góc độ quản lý dự án, **SmartHome Basic Kit** phải đối mặt với nhiều áp lực:
- Ngân sách hạn chế
- Thời gian triển khai ngắn
- Yêu cầu vừa đảm bảo chất lượng, vừa giữ giá thành thấp

Ngoài ra, hệ thống cần được thiết kế sao cho:
- Có khả năng mở rộng thêm thiết bị trong tương lai
- Không phải thay đổi toàn bộ kiến trúc ban đầu

Nếu kiến trúc hệ thống thiếu linh hoạt, chi phí nâng cấp và bảo trì về sau sẽ rất lớn.

---

## 3. Vấn đề kỹ thuật

### 3.1. Các vấn đề kỹ thuật chính

| Nhóm | Vấn đề | Phân tích |
|----|------|---------|
| Phần cứng | Thiết bị dễ lỗi | Linh kiện giá rẻ, sai số cảm biến |
| Mạng | Kết nối không ổn định | Wi-Fi gia đình yếu, nhiễu sóng |
| Phần mềm | Đồng bộ dữ liệu | Trạng thái thiết bị hiển thị sai |
| Hệ thống | Khả năng chịu tải | Nhiều thiết bị gửi dữ liệu cùng lúc |

---

### 3.2. Vấn đề về truyền thông và dữ liệu

Trong hệ thống SmartHome, dữ liệu giữa thiết bị và server được truyền liên tục. Nếu xảy ra các sự cố như:
- Gói tin bị mất
- Server phản hồi chậm
- Kết nối bị gián đoạn

Người dùng có thể gặp các hiện tượng:
- Bật/tắt thiết bị không có tác dụng
- Trạng thái hiển thị không đúng với thực tế

Điều này ảnh hưởng trực tiếp đến độ tin cậy và trải nghiệm sử dụng của hệ thống.

---

## 4. Vấn đề về Trải nghiệm Người dùng (UX/UI)

Một trong những thách thức lớn của **SmartHome Basic Kit** là thiết kế giao diện người dùng:
- Giao diện quá đơn giản → thiếu thông tin cần thiết
- Giao diện quá phức tạp → người dùng khó hiểu và khó thao tác

Ngoài ra:
- Thời gian phản hồi chậm khiến người dùng nghi ngờ hệ thống
- Thông báo lỗi không rõ ràng khiến người dùng không biết cách xử lý

Nếu UX/UI kém, dù hệ thống hoạt động đúng về mặt kỹ thuật, người dùng vẫn có xu hướng đánh giá thấp sản phẩm.

---

## 5. Vấn đề Quản lý Dự án

Dự án **SmartHome Basic Kit** yêu cầu sự phối hợp chặt chẽ giữa:
- Lập trình phần mềm
- Thiết kế phần cứng
- Kiểm thử thiết bị thực tế

Điều này gây khó khăn trong:
- Ước lượng tiến độ
- Phân công công việc
- Kiểm soát thay đổi yêu cầu

Đặc biệt, nếu yêu cầu thay đổi khi phần cứng đã được sản xuất, chi phí phát sinh sẽ rất lớn và khó kiểm soát.

---

# II. Phân tích Rủi ro Phát sinh

## 1. Rủi ro Kỹ thuật

| ID | Rủi ro | Nguyên nhân | Mức độ ảnh hưởng | Biện pháp |
|----|-------|------------|-----------------|----------|
| T1 | Mất kết nối thiết bị | Wi-Fi yếu | Cao | Tự động reconnect |
| T2 | Lỗi firmware | Kiểm thử chưa đầy đủ | Cao | OTA + rollback |
| T3 | Server quá tải | Nhiều thiết bị truy cập | Trung bình | Tối ưu backend |
| T4 | Mất dữ liệu | Sự cố hệ thống | Cao | Backup định kỳ |

---

## 2. Rủi ro Bảo mật

| ID | Rủi ro | Mức độ |
|----|-------|-------|
| S1 | Truy cập trái phép | Rất cao |
| S2 | Rò rỉ dữ liệu cá nhân | Cao |
| S3 | Giả mạo thiết bị IoT | Cao |

**Phân tích:**  
Hệ thống SmartHome liên quan trực tiếp đến an toàn không gian sống của người dùng. Chỉ một lỗ hổng bảo mật nhỏ cũng có thể dẫn đến hậu quả nghiêm trọng như điều khiển thiết bị trái phép hoặc xâm phạm quyền riêng tư.

---

## 3. Rủi ro Nghiệp vụ

Nếu sản phẩm:
- Không ổn định
- Khó sử dụng
- Có giá thành cao

Thì khả năng người dùng chấp nhận sản phẩm sẽ thấp, ảnh hưởng trực tiếp đến:
- Uy tín của dự án
- Khả năng thương mại hóa trong tương lai

---

## 4. Rủi ro Tiến độ và Chi phí

| ID | Rủi ro | Nguyên nhân | Biện pháp |
|----|-------|------------|----------|
| P1 | Trễ tiến độ | Chậm linh kiện | Dự phòng thời gian |
| P2 | Vượt chi phí | Phát sinh sửa lỗi | Dự trù ngân sách |
| P3 | Thiếu nhân lực | Thành viên nghỉ | Phân công chéo |

---

## 5. Rủi ro Vận hành và Bảo trì

Sau khi triển khai, hệ thống có thể gặp các vấn đề:
- Khó bảo trì nếu mã nguồn không được thiết kế theo hướng modular
- Khó nâng cấp nếu không hỗ trợ OTA
- Phụ thuộc vào các dịch vụ cloud của bên thứ ba

Nếu không được tính toán ngay từ giai đoạn thiết kế ban đầu, chi phí vận hành và bảo trì về sau sẽ rất cao.

**Kết luận:**  
Việc nhận diện sớm các vấn đề và rủi ro giúp dự án SmartHome Basic Kit chủ động xây dựng các biện pháp phòng ngừa, giảm thiểu tác động tiêu cực và nâng cao khả năng thành công khi triển khai thực tế.
```
