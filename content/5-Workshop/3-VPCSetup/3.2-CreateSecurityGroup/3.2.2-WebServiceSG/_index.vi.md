---
title : "Tạo Security Group cho Web Service"
date : "2025-10-10"
weight : 3
chapter : false
pre : " <b> 3.2.2. </b> "
---
Security Group này chỉ cho phép lưu lượng từ ALB tới các web server trên c cổng 80, đảm bảo nguyên tắc bảo mật "least privilege".

#### **Các bước thực hiện:**

1. **Truy cập trang Security Groups**
   - Điều hướng đến **EC2 Service** → **Security Groups**
   - Nhấp **Create security group**

2. **Cấu hình cơ bản**
   - **Tên Security Group:** `web-sg`
   - **Mô tả:** `Cho phép lưu lượng từ ALB tới web servers trên c cổng 80`
   - **VPC:** Chọn `advanced-alb-vpc`
   ![Cấu hình cơ bản](/images/3-VPCSetup/3.2-CreateSecurityGroup/3.2.2-WebServiceSG/01-BasicConfig.png)

3. **Thiết lập Inbound Rules**
   - Nhấp **Add rule** và cấu hình:
     - **Loại:** Custom HTTP
     - **Port range:** 80
     - **Nguồn:** Gõ `alb-sg` và chọn Security Group của ALB từ danh sách
   ![Cấu hình Inbound Rules](/images/3-VPCSetup/3.2-CreateSecurityGroup/3.2.2-WebServiceSG/02-InboundRule.png)

4. **Hoàn tất**
   - Nhấp **Create security group**