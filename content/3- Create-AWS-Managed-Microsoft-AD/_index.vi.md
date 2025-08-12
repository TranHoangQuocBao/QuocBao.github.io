| title       | date       | weight | chapter | prev |
|-------------|------------|--------|---------|------|
| Preparation | 2025-08-11 | 1      | false   | 1.   |
---
Bước 1 - Tạo AWS Managed Microsoft AD"
---

## Mục tiêu
Trong bước này, bạn sẽ tạo mới một AWS Managed Microsoft Active Directory (AD) trong tài khoản AWS của mình thông qua AWS Directory Service.

## Yêu cầu trước khi thực hiện
- Tài khoản AWS có đủ quyền (nên dùng **AdministratorAccess**).
- Đã cấu hình **VPC** với ít nhất hai subnet private ở hai Availability Zone khác nhau.

## Các bước thực hiện
1. **Mở AWS Management Console** và vào **Directory Service**.

2. Nhấn **Set up directory**.
![AWS Managed AD Step 1](D:\workshop\static\images\01\anh1.png)

3. Chọn **AWS Managed Microsoft AD** và nhấn **Next**.
![AWS Managed AD Step 1](D:\workshop\static\images\01\anh2.png)

4. Chọn **Edition**:
![AWS Managed AD Step 1](D:\workshop\static\images\01\anh3.png) 
   - **Standard Edition**: Tối đa 30.000 objects, phù hợp cho môi trường nhỏ.
   - **Enterprise Edition**: Tối đa 500.000 objects, phù hợp cho tổ chức lớn.

5. Nhập thông tin **Directory**:
![AWS Managed AD Step 1](D:\workshop\static\images\01\anh4.png)
   - **Directory DNS name**: ví dụ `corp.example.com`
   - **Directory NetBIOS name**: ví dụ `CORP`
   - **Admin password**: Đáp ứng yêu cầu độ phức tạp.

6. **Cấu hình VPC**:
![AWS Managed AD Step 1](D:\workshop\static\images\01\anh5.png)
   - Chọn **VPC**.
   - Chọn **hai subnet** ở hai Availability Zone khác nhau.

7. Kiểm tra lại cấu hình và nhấn **Create directory**.
![AWS Managed AD Step 1](D:\workshop\static\images\01\anh6.png)

8. Chờ trạng thái **Active** (khoảng 20–45 phút).
![AWS Managed AD Step 1](D:\workshop\static\images\01\anh7.png)


## Kết quả mong đợi
Một AWS Managed Microsoft AD đã được tạo, có thể truy cập trong VPC và sẵn sàng cho các cấu hình tiếp theo.

