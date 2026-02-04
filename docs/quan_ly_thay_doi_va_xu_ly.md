## 2. Quản Lý Thay Đổi và Xử Lý Vấn Đề Phát Sinh (Change & Issue Management Framework)

### 2.1. Mục Tiêu Quản Lý Thay Đổi

Quản lý thay đổi trong dự án **Smarthome Basic Kit** không chỉ nhằm kiểm soát phạm vi (scope control), mà còn nhằm:

* Ngăn chặn *scope creep* (phình to phạm vi không kiểm soát)
* Giảm **technical debt** (nợ kỹ thuật)
* Bảo toàn tính toàn vẹn kiến trúc hệ thống
* Duy trì tính nhất quán tài liệu dự án
* Liên kết chặt chẽ giữa **kỹ thuật – chi phí – tiến độ – rủi ro**

Mô hình quản lý thay đổi được triển khai theo **PMBOK + ITIL + Agile Hybrid Model**.

---

### 2.2. Cấu Trúc Quy Trình Quản Lý Thay Đổi (Change Control Workflow)

**Luồng xử lý chuẩn (Standard Change Flow):**

```text
Phát sinh nhu cầu thay đổi
        ↓
Gửi Change Request Form (CRF)
        ↓
Phân tích tác động (Impact Analysis)
        ↓
Hội đồng kiểm soát thay đổi (CCB Review)
        ↓
Phê duyệt / Từ chối / Trì hoãn
        ↓
Cập nhật tài liệu dự án
        ↓
Triển khai thay đổi
        ↓
Kiểm thử – xác nhận – đóng thay đổi
```

---

### 2.3. Biểu Mẫu Chuẩn: Change Request Form (CRF)

**CHANGE REQUEST FORM – Smarthome Basic Kit**

| Trường                      | Nội dung                                              |
| --------------------------- | ----------------------------------------------------- |
| CR ID                       | CR-ESP32-XXX                                          |
| Ngày yêu cầu                | dd/mm/yyyy                                            |
| Người yêu cầu               | Tên / bộ phận                                         |
| Loại thay đổi               | ☐ Kỹ thuật ☐ Phạm vi ☐ Chi phí ☐ Lịch trình ☐ Bảo mật |
| Mô tả thay đổi              | Mô tả chi tiết                                        |
| Lý do                       | Root cause / Business need / Risk mitigation          |
| Thành phần ảnh hưởng        | ☐ Firmware ☐ Hardware ☐ Cloud ☐ App ☐ Docs            |
| Phân tích tác động kỹ thuật | Architecture / Performance / Stability                |
| Phân tích chi phí           | +/- USD                                               |
| Phân tích tiến độ           | +/- tuần                                              |
| Phân tích rủi ro            | Low / Medium / High                                   |
| Phương án thay thế          | Alternative solutions                                 |
| Đề xuất                     | ☐ Approve ☐ Reject ☐ Defer                            |
| Người phê duyệt             | PM / Tech Lead / Sponsor                              |
| Trạng thái                  | Open / Approved / Implemented / Closed                |

---

### 2.4. Hội Đồng Kiểm Soát Thay Đổi (Change Control Board – CCB)

| Vai trò              | Trách nhiệm                           |
| ---------------      | ------------------------------------- |
| Quản lý dự án        | Kiểm soát phạm vi, ngân sách, tiến độ |
| Trưởng nhóm kỹ thuật | Đánh giá tác động kiến trúc           |
| Trưởng nhóm phần cứng| Đánh giá ảnh hưởng BOM/PCB            |
| Trưởng nhóm QA       | Đánh giá kiểm thử và độ ổn định       |
| Chủ Sản Phẩm         | Đánh giá giá trị người dùng           |

---

### 2.5. Phân Loại Thay Đổi (Change Classification)

**Theo mức độ ảnh hưởng:**

| Cấp độ              | Loại                      | Ví dụ                 |
| ---------------     | ------------------------- | --------------------- |
| Thay đổi nhỏ        | Không ảnh hưởng kiến trúc | Đổi tên biến, UI text |
| Thay đổi lớn        | Ảnh hưởng module          | Thay DHT11 → DHT22    |
| Thay Đổi Quan Trọng | Ảnh hưởng hệ thống        | Thay kiến trúc OTA    |

---

### 2.6. Ma Trận Phân Tích Tác Động (Impact Matrix)

| Yếu tố      | Trước thay đổi | Sau thay đổi | Tác động  |
| ----------- | -------------- | ------------ | --------- |
| Kiến trúc   | Monolithic     | Modular      | + ổn định |
| Chi phí BOM | $23–34         | $26–38       | +$3       |
| Độ tin cậy  | Trung bình     | Cao          | +++       |
| Bảo mật     | Thấp           | Trung bình   | ++        |
| Bảo trì     | Khó            | Dễ           | +++       |

---

### 2.7. Quản Lý Vấn Đề Phát Sinh (Issue Management System)

**Chu trình xử lý Issue:**

```text
Phát hiện sự cố
      ↓
Ghi nhận Issue Log
      ↓
Phân loại mức độ (Severity)
      ↓
Phân tích nguyên nhân gốc (RCA)
      ↓
Khắc phục tạm thời (Mitigation)
      ↓
Giải pháp lâu dài (Permanent Fix)
      ↓
Xác nhận – đóng issue
```

---

### 2.8. Biểu Mẫu Issue Log Chuẩn

| Issue ID | Mô tả                     | Severity | Nguyên nhân         | Giải pháp      | Trạng thái |
| -------- | ------------------------- | -------- | ------------------- | -------------- | ---------- |
| IS-01    | ESP32 reset khi bật relay | Critical | Brownout            | Thêm tụ 1000µF | Closed     |
| IS-02    | MQTT disconnect           | High     | WiFi stack blocking | Async MQTT     | Closed     |
| IS-03    | DHT11 NaN                 | Medium   | RTOS timing         | Retry logic    | Closed     |

---

### 2.9. Chuẩn Cập Nhật Tài Liệu (Documentation Governance)

Mỗi thay đổi được phê duyệt **bắt buộc cập nhật**:

| Tài liệu             | Trạng thái |
| -------------------- | ---------- |
| SRS                  | ✔          |
| SDD                  | ✔          |
| BOM                  | ✔          |
| WBS                  | ✔          |
| Sổ đăng ký rủi ro    | ✔          |
| Sơ đồ kiến trúc      | ✔          |
| Kế hoạch kiểm thử    | ✔          |
| Hướng dẫn sử dụng    | ✔          |
| OTA Policy           | ✔          |

---

### 2.10. Tích Hợp Với Quản Lý Phiên Bản (Version Control Integration)

**Quy ước version:**

```text
vMAJOR.MINOR.PATCH
```

**Ví dụ:**

* v1.0.0 – Bản ổn định đầu tiên
* v1.1.0 – Thêm automation rules
* v1.1.1 – Vá lỗi OTA

---

### 2.11. Liên Kết Quản Lý Thay Đổi với CI/CD

| Hành động                   | Tự động hóa         |
| ---------------             | ------------------  |
| Thay đổi đã được chấp thuận | Kích hoạt pipeline  |
| Hợp nhất mã nguồn           | Tự động xây dựng    |
| Kiểm tra thành công         | Tự động phát hành   |
| Triển khai                  | Triển khai OTA theo giai đoạn|

---

### 2.12. Mô Hình Chuẩn Hóa Quản Trị Dự Án

Hệ thống quản lý thay đổi được tích hợp theo mô hình:

**Mô hình quản trị:**

```text
PMBOK (Change Control)
+ ITIL (Incident / Problem Management)
+ DevOps (CI/CD)
+ Agile (Iterative delivery)
→ Hybrid Professional IoT Project Governance Model
```

---

## Kết Luận Học Thuật

Hệ thống quản lý thay đổi của dự án **Smarthome Basic Kit** đã được chuẩn hóa từ mô hình *dự án sinh viên / DIY* sang mô hình **quản trị dự án kỹ thuật chuyên nghiệp**, với các đặc trưng:

* Có biểu mẫu chính thức (CRF)
* Có hội đồng kiểm soát thay đổi (CCB)
* Có phân tích tác động đa chiều
* Có tích hợp CI/CD
* Có liên kết tài liệu hệ thống
* Có governance framework

➡️ Chuyển hóa dự án từ **Thực hiện dự án** → **Hệ thống Quản trị Dự án**
