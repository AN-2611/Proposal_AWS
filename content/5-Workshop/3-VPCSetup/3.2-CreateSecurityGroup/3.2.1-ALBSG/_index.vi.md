---
title : "Tạo Security Group cho ALB"
date : "2025-10-10"
weight : 2
chapter : false
pre : " <b> 3.2.1. </b> "
---
Security Group này cho phép lưu lượng web công cộng truy cập vào Application Load Balancer của bạn.

#### **Các bước thực hiện:**

1. **Truy cập EC2 Service**
   - Đăng nhập AWS Management Console
   - Tìm kiếm và chọn **EC2** từ thanh tìm kiếm

2. **Điều hướng đến Security Groups**
   - Trong menu bên trái, chọn **Security Groups** (dưới mục Network & Security)
   ![Màn hình Security Groups](/images/3-VPCSetup/3.2-CreateSecurityGroup/3.2.1-ALBSG/01-SGDashboard.png)

3. **Tạo Security Group mới**
   - Nhấp nút **Create security group**

4. **Cấu hình cơ bản**
   - **Tên Security Group:** `alb-sg`
   - **Mô tả:** `Cho phép lưu lượng HTTP và HTTPS công cộng cho ALB chính`
   - **VPC:** Chọn `advanced-alb-vpc`
   ![Cấu hình cơ bản](/images/3-VPCSetup/3.2-CreateSecurityGroup/3.2.1-ALBSG/02-BasicConfig.png)

5. **Thiết lập Inbound Rules (Quy tắc đầu vào)**
   - Nhấp **Add rule** và cấu hình:
     - **Loại:** HTTP (port 80)
     - **Nguồn:** Anywhere-IPv4 (0.0.0.0/0)
   - Nhấp **Add rule** lần nữa:
     - **Loại:** HTTPS (port 443)
     - **Nguồn:** Anywhere-IPv4 (0.0.0.0/0)
   ![Cấu hình Inbound Rules](/images/3-VPCSetup/3.2-CreateSecurityGroup/3.2.1-ALBSG/03-ConfigInboundRules.png)

6. **Cấu hình Outbound Rules (Quy tắc đầu ra)**
   - Giữ nguyên mặc định (Cho phép tất cả lưu lượng)

7. **Hoàn tất**
   - Nhấp **Create security group** để hoàn thành