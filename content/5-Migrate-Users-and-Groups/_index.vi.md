| title                      | date       | weight | chapter | prev |
|----------------------------|------------|--------|---------|------|
| 3-Migrate-Users-and-Groups | 2025-08-11 | 3      | false   | 1.   |
---
Bước 3 - Di chuyển Người dùng và Nhóm
---

## Mục tiêu
Bước này tập trung vào việc di chuyển người dùng và nhóm từ hệ thống Active Directory tại chỗ (on-premises) sang AWS Managed Microsoft AD.  
Quá trình này đảm bảo toàn bộ các đối tượng định danh được chuyển chính xác, giữ nguyên quyền truy cập, thành viên nhóm và chính sách mật khẩu.

---

## Yêu cầu trước khi thực hiện
Trước khi bắt đầu di chuyển:
- AWS Managed Microsoft AD đã được triển khai và kết nối được từ môi trường on-premises.
- Quan hệ tin cậy (trust relationship) giữa AWS Managed AD và AD tại chỗ đã được cấu hình và kiểm tra.
- Đã cài đặt các công cụ hỗ trợ di chuyển, bao gồm:
  - **Active Directory Migration Tool (ADMT)**.
  - **Password Export Server (PES)** nếu cần di chuyển mật khẩu.
- Tài khoản quản trị của cả hai miền (on-prem và AWS AD).

---

## Quy trình di chuyển

### 1. Cài đặt và cấu hình ADMT
- Cài ADMT trên máy chủ Windows là thành viên của miền AWS Managed AD.
- Đảm bảo máy chủ ADMT có thể giao tiếp với cả hai miền.
- Nếu di chuyển mật khẩu, cài **PES** trên Domain Controller của miền nguồn và cấu hình khóa mã hóa.

### 2. Lập kế hoạch di chuyển
- Xác định các Organizational Units (OU) cần di chuyển.
- Lập kế hoạch batch di chuyển:
  - Tài khoản quan trọng trước (quản trị viên, service accounts).
  - Người dùng thông thường.
  - Các nhóm bảo mật và phân phối.

### 3. Di chuyển tài khoản người dùng
- Sử dụng **User Account Migration Wizard** của ADMT để:
  - Chọn miền nguồn và miền đích.
  - Chọn tài khoản cần di chuyển.
  - Bật tùy chọn “Migrate associated user groups”.
  - Có thể di chuyển mật khẩu (yêu cầu PES).
- Kiểm tra log để đảm bảo không có lỗi.

### 4. Di chuyển nhóm
- Sử dụng **Group Migration Wizard** của ADMT để:
  - Giữ nguyên loại nhóm (Global, Universal, Domain Local).
  - Bảo toàn danh sách thành viên.

### 5. Kiểm tra sau di chuyển
- Đăng nhập bằng tài khoản đã di chuyển để xác nhận xác thực trên AWS AD.
- Kiểm tra quyền truy cập và thành viên nhóm.
- Cập nhật các ứng dụng/dịch vụ để dùng AWS Managed Microsoft AD.

---

## Best Practices
- Thực hiện **pilot migration** trước khi di chuyển toàn bộ.
- Sao lưu cả hai môi trường AD trước khi thực hiện.
- Lên lịch di chuyển ngoài giờ cao điểm.
- Ghi chép chi tiết tất cả đối tượng đã di chuyển để phục vụ kiểm tra và rollback.
