| title       | date       | weight | chapter | prev |
|-------------|------------|--------|---------|------|
| Preparation | 2025-08-11 | 2      | false   | 1.   |
---
Bước 2 – Cấu hình Trust Relationships
---

## Tổng quan
Ở bước này, chúng ta sẽ thiết lập **mối quan hệ tin cậy (trust relationships)** giữa AWS Managed Microsoft AD và Active Directory tại chỗ (on-premises). Điều này giúp xác thực người dùng liền mạch, chia sẻ tài nguyên và triển khai Single Sign-On (SSO) giữa các môi trường.

## Mục tiêu
- Cho phép xác thực người dùng an toàn giữa AWS và AD tại chỗ.
- Giúp người dùng truy cập tài nguyên AWS bằng thông tin đăng nhập sẵn có.
- Hỗ trợ quản lý danh tính trong môi trường lai (hybrid identity management).

## Yêu cầu chuẩn bị
Trước khi cấu hình trust relationships, cần đảm bảo:
- AWS Managed Microsoft AD đã được tạo thành công ở Bước 1.
- Có tài khoản quản trị cho cả AWS Managed AD và AD tại chỗ.
- Đã thiết lập kết nối mạng (VPC Peering hoặc VPN/Direct Connect) giữa AWS và on-prem.
- Đã mở các port cần thiết cho Active Directory trust (ví dụ: TCP/UDP 88, 389, 445…).

## Quy trình thực hiện

### 1. Truy cập AWS Directory Service
1. Đăng nhập vào AWS Management Console.
2. Truy cập **Directory Service** → chọn AWS Managed Microsoft AD của bạn.
![Configure Trust Relationships](D:\workshop\static\images\1\01.png)
### 2. Tạo Trust Relationship
1. Trong giao diện AD, chọn **Networking & security** → **Trust relationships**.
![Configure Trust Relationships](D:\workshop\static\images\1\02.png)

2. Nhấn **Add trust**.
![Configure Trust Relationships](D:\workshop\static\images\1\03.png)

3. Chọn hướng trust:
   - **One-way incoming** – AD tại chỗ tin cậy AWS Managed AD.
   - **One-way outgoing** – AWS Managed AD tin cậy AD tại chỗ.
   - **Two-way** – Hai bên tin cậy lẫn nhau.
4. Chọn loại trust **Forest trust** để hỗ trợ xác thực đa domain.
![Configure Trust Relationships](D:\workshop\static\images\1\03.png)

### 3. Cấu hình chi tiết trust
- Nhập **FQDN** của domain cần trust.
- Đặt mật khẩu trust (giống nhau ở cả hai phía).
- Chọn **Selective authentication** để bảo mật cao hơn, hoặc **Forest-wide authentication** để tiện truy cập.
![Configure Trust Relationships](D:\workshop\static\images\1\04.png)

### 4. Xác nhận và kiểm tra trust
![Configure Trust Relationships](D:\workshop\static\images\1\05.png)
- Nhấn **Create** và chờ quá trình tạo hoàn tất.
- Từ AD tại chỗ, cấu hình trust tương ứng trong **Active Directory Domains and Trusts**.
- Kiểm tra trust từ cả hai phía để đảm bảo kết nối.

## Best Practices
- Ưu tiên dùng **two-way trust** nếu không bị giới hạn bởi chính sách bảo mật.
- Áp dụng **conditional access policies** để giới hạn truy cập theo nhóm người dùng.
- Theo dõi tình trạng trust định kỳ qua AWS Directory Service logs và CloudWatch.

## Kết quả
Hoàn thành bước này, AWS Managed Microsoft AD và AD tại chỗ sẽ được kết nối tin cậy, cho phép chia sẻ tài nguyên và xác thực người dùng giữa hai môi trường.
