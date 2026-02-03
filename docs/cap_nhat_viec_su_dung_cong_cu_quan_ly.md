# 8. CẬP NHẬT VIỆC SỬ DỤNG CÔNG CỤ QUẢN LÝ DỰ ÁN VÀ KHAI THÁC DASHBOARD BÁO CÁO

## 8.1. Lựa chọn và triển khai công cụ quản lý dự án

Để kiểm soát **tiến độ, chi phí và rủi ro** của dự án **Smarthome Basic Kit**, nhóm sử dụng **công cụ quản lý dự án số (GitHub)** nhằm chuẩn hóa việc lập kế hoạch, theo dõi và báo cáo.

Công cụ được cấu hình xoay quanh **3 trụ cột chính**:

- **Quản lý tiến độ (Schedule Management)**
- **Quản lý khối lượng công việc (Workload & WBS)**
- **Theo dõi hiệu suất (Performance Tracking – KPI, EVM)**

Việc áp dụng công cụ không chỉ phục vụ quản trị vận hành mà còn đóng vai trò **nguồn dữ liệu đầu vào** cho các phân tích định lượng trong báo cáo như **SPI, CPI, EV, PV, AC**.

---

## 8.2. Thiết lập cấu trúc dữ liệu trên công cụ (Tool Configuration)

### 8.2.1. Chuẩn hóa WBS và Task Hierarchy

- Mỗi hạng mục trong **WBS** (Thiết kế PCB, Firmware, Provisioning, Kiểm thử, …) được ánh xạ thành **Epic / Summary Task**.
- Các công việc chi tiết (ví dụ: *Xử lý brownout ESP32*, *Tích hợp MQTT reconnect logic*) được thiết lập dưới dạng **Task / Sub-task**.
- Mỗi task đều được gắn đầy đủ thông tin:
  - Thời gian kế hoạch (*Planned Duration*)
  - Người phụ trách
  - Trạng thái (*To Do / In Progress / Done*)
  - Phụ thuộc logic (*Finish-to-Start*)

Cách tổ chức này cho phép công cụ tự động **phát hiện điểm nghẽn (critical path)** và các công việc gây trễ dây chuyền.

---

## 8.3. Dashboard theo dõi tiến độ và sức khỏe dự án

### 8.3.1. Dashboard tiến độ tổng thể (Project Progress Dashboard)

Dashboard thể hiện các chỉ số:

- Tỷ lệ hoàn thành tổng thể (*Overall Completion Rate*)
- Số lượng task trễ hạn (*Overdue Tasks*)
- Phân bổ trạng thái công việc (*To Do / Doing / Done*)

**Ý nghĩa quản trị:**  
Dashboard cho phép đối chiếu trực quan giữa **kế hoạch ban đầu (baseline)** và **thực tế triển khai**, làm cơ sở xác định sai lệch tiến độ đã được phân tích với **SPI ≈ 0.8**.

---

### 8.3.2. Dashboard phân bổ nguồn lực (Resource & Workload Dashboard)

- Biểu đồ workload thể hiện **số giờ làm việc/tuần** của từng thành viên.
- Công cụ giúp phát hiện:
  - Hiện tượng **dồn tải vào firmware engineer** trong giai đoạn tích hợp
  - **Thiếu phân bổ thời gian cho kiểm thử sớm** (*testing gaps*)

**Liên hệ với báo cáo:**  
Dashboard này lý giải nguyên nhân quy trình dẫn đến **debug loop kéo dài** và **hiệu suất thấp** trong giai đoạn **tuần 9–12** của dự án.

---

## 8.4. Khai thác báo cáo hiệu suất (EVM & KPI Reporting)

### 8.4.1. Báo cáo Earned Value Management (EVM)

Từ dữ liệu task và tỷ lệ hoàn thành, công cụ cho phép xuất tự động:

- **Planned Value (PV)**
- **Earned Value (EV)**
- **Actual Cost (AC)**

Các chỉ số tổng hợp:

- **SPI ≈ 0.8**
- **CPI ≈ 0.75**

Hệ thống báo cáo đảm bảo:

- Tính **khách quan**
- Khả năng **truy vết (traceability)** từ chỉ số → task → nguyên nhân

Điều này chứng minh nhóm **không tính toán thủ công cảm tính**, mà dựa trên **hệ thống dữ liệu quản trị dự án thực tế**.

---

### 8.4.2. KPI Dashboard

Các **KPI chính** được theo dõi liên tục bao gồm:

- Tỷ lệ task hoàn thành đúng hạn (*On-time Completion Rate*)
- Số lỗi tích hợp giữa hardware – firmware
- Số lần rework PCB / firmware

**Vai trò trong báo cáo:**  
Dashboard KPI là cơ sở để:

- Dự báo **EAC (Estimate at Completion)** và **ETC (Estimate to Complete)**
- Ra quyết định **cắt giảm phạm vi (scope trimming)** hoặc **giãn tiến độ**

---

## 8.5. Trích xuất dữ liệu phục vụ báo cáo và minh họa

Công cụ quản lý cho phép:

- Xuất dữ liệu **Excel / CSV**:
  - Danh sách task
  - Timeline
  - Chi phí thực tế
- Xuất **ảnh dashboard** để minh họa trực tiếp trong báo cáo

**Giá trị học thuật & thực tiễn:**

- Báo cáo mang tính **data-backed**, không chỉ mô tả định tính
- Thể hiện rõ năng lực:
  - Sử dụng công cụ quản lý dự án hiện đại
  - Phân tích dự án dựa trên số liệu
  - Kết nối giữa **quản trị dự án** và **kỹ thuật IoT**

---

## 8.6. Đánh giá mức độ làm chủ công nghệ quản lý dự án

Việc sử dụng hiệu quả dashboard và báo cáo cho thấy nhóm đã:

- Chuyển từ **quản lý thủ công** sang **quản lý dựa trên dữ liệu**
- Áp dụng đúng tinh thần **Project Management hiện đại**
- Kết nối chặt chẽ giữa:

**Công cụ quản lý ⟷ Dữ liệu ⟷ Phân tích ⟷ Quyết định**

Đây là yếu tố tạo nên sự khác biệt rõ ràng giữa **một báo cáo sinh viên thông thường** và **một báo cáo mang tư duy triển khai dự án thực tế**.
