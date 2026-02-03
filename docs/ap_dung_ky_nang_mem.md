## 5. Áp dụng Kỹ năng mềm trong Quản lý Xung đột và Tạo động lực nhóm

---

### 5.1. Bối cảnh xung đột trong dự án Smarthome Basic Kit

Dựa trên các phân tích ở **Phần 1** (EVM, SPI, CPI, Technical Debt), dự án **Smarthome Basic Kit** tồn tại nhiều điều kiện dễ phát sinh xung đột nội bộ:

* **Áp lực tiến độ:** SPI = 0.8 → trễ tiến độ ~20%
* **Áp lực chi phí:** CPI = 0.75 → vượt ngân sách
* **Căng thẳng kỹ thuật:**

  * Reset ESP32 (brownout)
  * Lỗi DHT11 (NaN)
  * Provisioning phức tạp
  * MQTT disconnect
* **Bất đối xứng kỳ vọng giữa các bên:**

  * Nhóm kỹ thuật → ưu tiên ổn định hệ thống, kiến trúc bền vững
  * Nhóm quản lý / điều phối → ưu tiên tiến độ, mốc bàn giao, báo cáo
  * Người dùng thử nghiệm → ưu tiên trải nghiệm, độ ổn định, dễ sử dụng

➡️ Hình thành **xung đột đa tầng**:

* Xung đột chuyên môn (Technical conflict)
* Xung đột mục tiêu (Goal conflict)
* Xung đột tâm lý – cảm xúc (Emotional conflict)
* Xung đột vai trò (Role conflict)

---

### 5.2. Phân tích các dạng xung đột điển hình

#### 5.2.1. Xung đột kỹ thuật – quản lý (Technical vs Management Conflict)

**Tình huống thực tế:**

* Nhóm firmware cần thêm thời gian xử lý lỗi brownout/reset, provisioning, MQTT reconnect.
* Nhóm quản lý yêu cầu giữ mốc thời gian theo kế hoạch ban đầu.

**Biểu hiện:**

* Tranh luận giữa *"kỹ thuật"* và *"deadline"*
* Đổ lỗi qua lại:

  * Quản lý: *"Dev code không ổn định"*
  * Dev: *"Kế hoạch phi thực tế"*

**Nguy cơ:**

* Mất niềm tin giữa các vai trò
* Hình thành tâm lý phòng thủ thay vì hợp tác
* Giảm động lực nội tại của kỹ sư

---

#### 5.2.2. Xung đột trong nhóm kỹ thuật (Internal Team Conflict)

**Nguyên nhân:**

* Gỡ lỗi kéo dài
* Lỗi lặp đi lặp lại (reset, NaN sensor, network fail)
* Technical debt gia tăng

**Biểu hiện:**

* Kiệt sức tinh thần (burnout nhẹ)
* Tránh trách nhiệm
* Làm việc đối phó, giảm sáng tạo

---

#### 5.2.3. Xung đột giá trị (Value Conflict)

**Ví dụ:**

* Một nhóm ưu tiên: *"làm cho xong, chạy được"*
* Nhóm khác ưu tiên: *"làm cho chuẩn, bền, scalable"*

➡️ Đây là **khác biệt hệ giá trị nghề nghiệp**, không chỉ là khác quan điểm kỹ thuật.

---

### 5.3. Khung kỹ năng mềm áp dụng (Soft Skills Framework)

Quản lý xung đột không dựa trên quyền lực hay mệnh lệnh, mà dựa trên **4 trụ cột kỹ năng mềm**:

#### (1) Trí tuệ cảm xúc (Emotional Intelligence – EQ)

* Nhận diện cảm xúc của cá nhân và tập thể
* Kiểm soát phản ứng cá nhân
* Đồng cảm với áp lực của các vai trò khác

#### (2) Giao tiếp chiến lược (Strategic Communication)

* Giao tiếp dựa trên dữ liệu (SPI, CPI, EAC, ETC)
* Tránh giao tiếp cảm tính
* Sử dụng ngôn ngữ trung lập, không đổ lỗi

#### (3) Tư duy hệ thống (Systems Thinking)

* Nhìn dự án như một hệ sinh thái
* Không tách rời kỹ thuật – con người – quy trình – tài chính

#### (4) Lãnh đạo phục vụ (Servant Leadership)

* Lãnh đạo với vai trò hỗ trợ đội ngũ thành công
* Không tập trung kiểm soát vi mô

---

### 5.4. Chiến lược quản lý xung đột

#### 5.4.1. Chuyển từ “đổ lỗi” sang “phân tích hệ thống”

**Không hỏi:**

> Ai làm sai?

**Mà hỏi:**

> Cơ chế nào của hệ thống tạo ra lỗi này?

**Ví dụ:**

* Reset ESP32 → không quy cho dev → quy cho thiết kế nguồn
* DHT11 trả về NaN → không quy cho code → quy cho kiến trúc RTOS + cảm biến

➡️ Chuyển xung đột cá nhân thành vấn đề kỹ thuật hệ thống.

---

#### 5.4.2. Quản lý xung đột bằng dữ liệu (Data-driven Conflict Management)

Sử dụng:

* SPI, CPI
* EAC, ETC
* Risk Register
* Technical Debt List

➡️ Biến tranh luận cảm xúc thành phân tích định lượng.

---

#### 5.4.3. Tách con người khỏi vấn đề (Principled Negotiation)

Áp dụng mô hình **Harvard Negotiation**:

* Tách *people* khỏi *problem*
* Tập trung vào *interests* thay vì *positions*
* Tìm giải pháp **win–win**

**Ví dụ:**

* Interest của dev: hệ thống ổn định
* Interest của quản lý: tiến độ, bàn giao

➡️ Giải pháp: chia nhỏ release:

* v1.0: core function
* v1.1: automation nâng cao

---

### 5.5. Chiến lược tạo động lực (Motivation Strategy)

#### 5.5.1. Động lực nội tại (Intrinsic Motivation)

Tạo cảm giác:

* **Năng lực (Competence):** được làm kỹ thuật đúng chuẩn
* **Tự chủ (Autonomy):** được đề xuất và quyết định giải pháp
* **Ý nghĩa (Purpose):** sản phẩm có giá trị thực tiễn

---

#### 5.5.2. Động lực ngoại tại (Extrinsic Motivation)

* Công nhận đóng góp kỹ thuật
* Minh bạch đánh giá hiệu suất
* Ghi nhận nỗ lực vượt khó

---

#### 5.5.3. Chuyển áp lực thành động lực phát triển

Không coi:

> Trễ tiến độ, vượt ngân sách = thất bại

Mà coi là:

> Giai đoạn học tập tăng tốc (*accelerated learning phase*)

➡️ Xây dựng văn hóa học tập, không phải văn hóa trừng phạt.

---

### 5.6. Giải pháp tổ chức mang tính dài hạn

#### 5.6.1. Thiết kế cơ chế phòng ngừa xung đột

* Retrospective định kỳ
* Risk Review Meeting
* Technical Review Board
* Sprint Reflection

---

#### 5.6.2. Thể chế hóa giao tiếp

* Chuẩn hóa báo cáo kỹ thuật
* Chuẩn hóa họp kỹ thuật và họp quản lý
* Phân tách họp giải pháp và họp tiến độ

---

#### 5.6.3. Xây dựng văn hóa đội nhóm

Văn hóa cốt lõi:

* Không đổ lỗi
* Minh bạch
* Học hỏi
* Hợp tác liên vai trò (*cross-functional*)

---

### 5.7. Giá trị chiến lược của kỹ năng mềm trong dự án công nghệ

Trong các dự án IoT, rủi ro kỹ thuật là không thể tránh khỏi, nhưng:

> Thất bại dự án hiếm khi đến từ công nghệ,
> mà đến từ xung đột con người không được quản lý đúng cách.

**Vai trò của kỹ năng mềm:**

| Kỹ năng mềm      | Tác động hệ thống      |
| ---------------- | ---------------------- |
| Giao tiếp        | Giảm hiểu sai kỹ thuật |
| Đồng cảm         | Giảm căng thẳng        |
| Lãnh đạo         | Tăng niềm tin          |
| Quản lý xung đột | Giữ gắn kết            |
| Tạo động lực     | Duy trì hiệu suất      |

---

### 5.8. Kết luận học thuật

Việc áp dụng kỹ năng mềm trong dự án **Smarthome Basic Kit** không chỉ nhằm giải quyết xung đột trước mắt, mà còn:

* Ổn định tâm lý tổ chức
* Duy trì hiệu suất dài hạn
* Giảm **technical debt xã hội** (*social technical debt*)
* Tạo nền tảng cho phát triển bền vững
