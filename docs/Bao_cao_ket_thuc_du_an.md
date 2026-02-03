# Phần 3: Báo Cáo Kết Thúc Dự Án và Bài Học Kinh Nghiệm

## 3.1 Trạng Thái Hoàn Thành Dự Án

-   **Sản Phẩm Bàn Giao**: Nguyên mẫu phần cứng, mã nguồn v1.0, tài liệu
    hướng dẫn đã hoàn tất.
-   **Tài Chính**: Chi phí thực tế **\$4,000** (vượt ngân sách nếu tính
    cả công nợ kỹ thuật).
-   **Chấp Nhận**: Chức năng cốt lõi đã qua UAT; các quy tắc nâng cao
    dời sang v1.1.

## 3.2 Bài Học Kinh Nghiệm (Post-Mortem Analysis)

### 3.2.1 Bài Học Về Kỹ Thuật

-   **Tính Toàn Vẹn Của Nguồn Cung Cấp Điện**\
    Nguồn USB không đủ ổn định.\
    **Bài học**: Luôn tạo mẫu với nguồn điện mục tiêu và bắt buộc thêm
    tụ điện (470µF/1000µF) song song với đường ray nguồn để bù đắp gai
    dòng điện.

-   **Lựa Chọn Cảm Biến**\
    DHT11 rẻ nhưng không đáng tin cậy.\
    **Bài học**: Sử dụng DHT22 hoặc BME280 cho các logic vòng điều khiển
    quan trọng.

### 3.2.2 Bài Học Về Quy Trình

-   **Giới Hạn Của IDE**\
    Arduino IDE không quản lý tốt dự án lớn.\
    **Bài học**: Chuyển sang PlatformIO (VS Code) để quản lý mô-đun và
    phụ thuộc tốt hơn.

-   **Khoảng Trống Trong Kiểm Thử**\
    Kiểm thử thủ công để lọt lỗi.\
    **Bài học**: Triển khai kiểm thử đơn vị tự động (Automated Unit
    Testing) qua GitHub Actions.

## 3.3 Kiến Nghị Cải Tiến Quy Trình Cho Tương Lai

-   **Triển Khai CI/CD**: Tự động hóa Builds, Lints, Tests (mô phỏng
    QEMU) và Releases.
-   **Củng Cố Bảo Mật**: Loại bỏ mật khẩu mặc định, bật Mã hóa Flash /
    Secure Boot và sử dụng TLS/SSL cho MQTT.
-   **Quy Trình Cung Cấp Nâng Cao**: Sử dụng Espressif Wi-Fi
    Provisioning Manager qua Bluetooth LE để tăng tính chuyên nghiệp và
    bảo mật.

## Phân Tích Chi Tiết và Lý Luận Bối Cảnh

-   **Kinh Tế Học Của "Basic Kit"**\
    Sự vượt chi ngân sách phản ánh *Thiên kiến Lạc quan*. Phân tích Chi
    phí Chất lượng (COQ) cho thấy việc nâng cấp BOM thêm **\$5** có thể
    tiết kiệm **\$2,000** chi phí khắc phục lỗi sau này.

-   **Sự Đánh Đổi Giữa Bảo Mật và Khả Dụng**\
    Việc sử dụng Wi-Fi AP mở để thiết lập là rủi ro. Chuyển sang cung
    cấp qua Bluetooth tạo ra lớp bảo mật *"Bằng chứng sở hữu"*.

-   **Từ "Mã Nguồn" Đến "Sản Phẩm"**\
    Chuyển đổi sang PlatformIO không chỉ là thay đổi công cụ mà là thay
    đổi văn hóa, giúp ngăn chặn tình trạng *"thối mã"* và đảm bảo khả
    năng tái tạo môi trường.
