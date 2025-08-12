| title                              | date       | weight | chapter | prev |
|------------------------------------|------------|--------|---------|------|
| Giám sát và Xác minh Tích hợp      | 2025-08-11 | 5      | false   | 1.   |
---
5 - Giám sát và Xác minh Tích hợp
---

## Mục tiêu
Đảm bảo tích hợp AWS Managed Microsoft AD với hệ thống AD tại chỗ hoặc trên cloud hoạt động đúng yêu cầu về bảo mật, tuân thủ và hiệu năng.

---

## Các bước thực hiện

### 1. Thiết lập công cụ giám sát
- **Amazon CloudWatch**: Theo dõi chỉ số về tình trạng dịch vụ, trạng thái trust, và quá trình replication.
- **AWS CloudTrail**: Ghi nhận và xem lại các thay đổi trong môi trường AD.
- **AWS Directory Service Console**: Kiểm tra trạng thái và nhật ký.

### 2. Xác minh Trust Relationship
- Sử dụng **Active Directory Domains and Trusts** để xác nhận trust đã được thiết lập và hoạt động.
- Chạy lệnh `nltest /sc_query:<TrustedDomain>` để kiểm tra kênh bảo mật.

### 3. Kiểm tra hoạt động của User và Group
- Thử đăng nhập người dùng từ cả hai môi trường.
- Xác nhận đồng bộ nhóm và quyền.

### 4. Kiểm tra Chính sách Bảo mật
- Đảm bảo Group Policy Objects (GPOs) áp dụng đúng.
- Kiểm tra chính sách mật khẩu và cấu hình MFA.

### 5. Tuân thủ và Kiểm toán
- Xem lại log để phát hiện truy cập trái phép.
- Đảm bảo dữ liệu và cấu hình đáp ứng tiêu chuẩn (ISO, SOC, HIPAA, ...).

---

## Thực hành tốt nhất
- Bật cảnh báo CloudWatch cho các lỗi trust hoặc replication.
- Thiết lập kiểm tra tự động định kỳ.
- Ghi lại toàn bộ kết quả và điều chỉnh.

---

## Ví dụ lệnh

```powershell
# Kiểm tra trust
nltest /sc_query:corp.example.com

# Kiểm tra tình trạng replication
repadmin /replsummary
