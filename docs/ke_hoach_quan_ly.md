## 3. Hoàn Thiện Kế Hoạch Quản Lý Chất Lượng và Kiểm Thử

### (Quality Management & Comprehensive Testing Master Plan)

---

### 3.1. Mục tiêu Quản lý Chất lượng (Quality Objectives)

Kế hoạch quản lý chất lượng của hệ thống **Smarthome Basic Kit** được xây dựng không chỉ để đảm bảo hệ thống *hoạt động được*, mà nhằm đảm bảo:

* **Tính ổn định dài hạn** (*Long-term Stability*)
* **Độ tin cậy vận hành** (*Operational Reliability*)
* **Tính an toàn** (*Safety & Electrical Safety*)
* **Khả năng mở rộng** (*Scalability*)
* **Khả năng thương mại hóa** (*Commercial-readiness*)

Chất lượng được tiếp cận theo mô hình **Total Quality Management (TQM)**, kết hợp:

* ISO 9001 – Quality Management System
* ISO/IEC 25010 – Software Quality Model
* ISTQB – Testing Framework
* DevOps Quality Engineering

---

### 3.2. Khung Quản Lý Chất Lượng (Quality Governance Framework)

**Mô hình kiểm soát chất lượng tổng thể:**

```text
Quality Planning  →  Quality Assurance  →  Quality Control  →  Quality Improvement
```

**Cấu trúc quản trị chất lượng:**

| Vai trò          | Trách nhiệm                    |
| ---------------- | ------------------------------ |
| Project Manager  | Chính sách chất lượng tổng thể |
| QA Lead          | Chuẩn hóa quy trình kiểm thử   |
| Technical Lead   | Kiểm soát chất lượng kiến trúc |
| Firmware Lead    | Code quality, memory safety    |
| Hardware Lead    | Electrical safety, EMC         |
| Security Officer | An toàn thông tin              |

---

### 3.3. Mô hình Chất lượng Hệ thống (ISO/IEC 25010 Mapping)

| Thuộc tính             | Áp dụng cho Smarthome      |
| ---------------------- | -------------------------- |
| Functional Suitability | Relay, Sensor, Automation  |
| Performance Efficiency | MQTT latency, Web response |
| Compatibility          | MQTT, Home Assistant       |
| Usability              | Provisioning, UI           |
| Reliability            | Reboot rate, uptime        |
| Security               | OTA, TLS, Authentication   |
| Maintainability        | Modular firmware           |
| Portability            | ESP32 variants             |

---

### 3.4. Kế Hoạch Kiểm Thử Toàn Diện (Master Test Plan)

#### 3.4.1. Chiến lược kiểm thử đa tầng (Multi-layer Testing Strategy)

```text
Unit Test → Integration Test → System Test → Acceptance Test → Operational Test
```

---

#### 3.4.2. Kiểm thử Chức năng (Functional Testing)

**Phạm vi kiểm thử:**

* Relay control (điều khiển thiết bị)
* Sensor reading (thu thập dữ liệu cảm biến)
* Web-based dashboard
* MQTT publish / subscribe
* Provisioning (cấu hình mạng)
* Automation rules

**Test case mẫu:**

| ID    | Mô tả               | Kết quả mong đợi    |
| ----- | ------------------- | ------------------- |
| FT-01 | Bật relay từ Web UI | Relay ON < 300ms    |
| FT-02 | MQTT publish sensor | Broker nhận dữ liệu |
| FT-03 | WiFi reconnect      | Reconnect < 60s     |
| FT-04 | Automation rule     | Trigger đúng logic  |

---

### 3.5. Kiểm Thử Phi Chức Năng (Non-Functional Testing)

#### 3.5.1. Kiểm thử Hiệu năng (Performance Testing)

**Chỉ số đánh giá:**

| Tiêu chí          | Ngưỡng chấp nhận |
| ----------------- | ---------------- |
| Web response time | < 500 ms         |
| MQTT latency      | < 300 ms         |
| Boot time         | < 8 s            |
| WiFi reconnect    | < 60 s           |
| OTA update        | < 120 s          |

**Stress Test:**

* 1000 MQTT messages/hour
* Relay switching 10.000 cycles
* Continuous OTA simulation

---

#### 3.5.2. Kiểm thử Độ tin cậy (Reliability Testing)

| Tiêu chí           | Chuẩn nghiệm thu |
| ------------------ | ---------------- |
| Spontaneous reboot | ≤ 1 / 72h        |
| Memory leak        | Heap ổn định     |
| Brownout           | 0 events         |
| Watchdog reset     | 0                |

---

#### 3.5.3. Kiểm thử Bảo mật (Security Testing)

| Hạng mục           | Phương pháp      |
| ------------------ | ---------------- |
| Auth bypass        | Penetration test |
| OTA tampering      | Hash verify      |
| MQTT sniffing      | TLS validation   |
| Firmware injection | Secure Boot      |
| Flash readout      | Flash encryption |

---

#### 3.5.4. Kiểm thử An toàn điện (Electrical Safety Testing)

| Hạng mục             | Tiêu chuẩn  |
| -------------------- | ----------- |
| Cách ly relay        | Optocoupler |
| Creepage / Clearance | IPC-2221    |
| Grounding            | IEC Safety  |
| Thermal              | < 60°C      |

---

### 3.6. Kế Hoạch Kiểm Thử Chấp Nhận Người Dùng (UAT)

#### 3.6.1. Mục tiêu UAT

* Xác nhận giá trị sử dụng thực tế
* Xác nhận độ ổn định
* Xác nhận trải nghiệm người dùng
* Xác nhận an toàn vận hành

---

#### 3.6.2. Kịch bản UAT chuẩn

**Kịch bản 1 – Công tắc thông minh:**

* Bật/tắt relay
* Không reset ESP32
* Không delay > 1s

**Kịch bản 2 – Giám sát môi trường:**

* Đọc nhiệt độ/độ ẩm
* So sánh nhiệt kế chuẩn
* Sai số < ±2°C

**Kịch bản 3 – Tự động hóa:**

* Rule-based automation
* Hoạt động offline

**Kịch bản 4 – Provisioning:**

* Người dùng mới cấu hình WiFi
* Không hardcode
* Không lỗi kết nối

---

#### 3.6.3. Tiêu chí nghiệm thu UAT (Acceptance Criteria)

| Nhóm        | Tiêu chí                |
| ----------- | ----------------------- |
| Chức năng   | 100% core features pass |
| Hiệu năng   | Đạt SLA                 |
| Ổn định     | Uptime ≥ 99%            |
| Bảo mật     | Không auth bypass       |
| An toàn     | Không sự cố điện        |
| Trải nghiệm | User rating ≥ 4/5       |

---

### 3.7. Quy trình Kiểm thử Tự động (Automated Testing Framework)

**Pipeline kiểm thử:**

```text
Commit → Build → Unit Test → Static Analysis → Firmware Test → Release
```

**Công cụ sử dụng:**

* PlatformIO
* Unity Test Framework
* GitHub Actions
* QEMU ESP32
* MQTT Test Broker

---

### 3.8. Quản lý lỗi và Truy vết Chất lượng (Defect & Traceability Management)

**Defect lifecycle:**

```text
Open → Triaged → Fixed → Tested → Verified → Closed
```

**Traceability Matrix (RTM):**

| Requirement   | Test Case | Status |
| ------------- | --------- | ------ |
| Relay Control | FT-01     | Pass   |
| MQTT          | FT-02     | Pass   |
| OTA           | ST-05     | Pass   |
| Security      | SEC-01    | Pass   |

---

### 3.9. Chuẩn Báo Cáo Chất lượng (Quality Metrics Dashboard)

| KPI            | Ngưỡng     |
| -------------- | ---------- |
| Test coverage  | ≥ 80%      |
| Defect density | < 0.5 / FP |
| MTBF           | > 72h      |
| Reboot rate    | < 1 / 72h  |
| OTA success    | > 99%      |

---

## Kết Luận Học Thuật

Kế hoạch quản lý chất lượng và kiểm thử của **Smarthome Basic Kit** đã được nâng cấp từ mức *dự án sinh viên / DIY* lên chuẩn **hệ thống kỹ thuật chuyên nghiệp**, với các đặc trưng:

* Kiểm thử đa tầng (*multi-layer testing*)
* Kiểm thử phi chức năng đầy đủ
* Kiểm thử bảo mật hệ thống
* Kiểm thử an toàn điện
* UAT chuẩn hóa
* CI/CD tích hợp kiểm thử
* Traceability đầy đủ
* Quality governance
