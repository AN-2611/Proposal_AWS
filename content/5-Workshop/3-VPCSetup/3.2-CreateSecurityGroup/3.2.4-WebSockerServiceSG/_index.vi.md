---
title : "Tạo Security Group cho WebSocket Service"
date : "2025-10-10"
weight : 4
chapter : false
pre : " <b> 3.2.4. </b> "
---

Security Group này chỉ cho phép lưu lượng từ ALB tới các WebSocket servers trên cổng 3000, đảm bảo tính bảo mật và hiệu suất cho các kết nối WebSocket.

#### **Các bước thực hiện:**

1. **Truy cập trang Security Groups**
   - Điều hướng đến **EC2 Service** → **Security Groups**
   - Nhấp **Create security group**

2. **Cấu hình cơ bản**
   - **Tên Security Group:** `websocket-sg`
   - **Mô tả:** `Cho phép lưu lượng từ ALB tới WebSocket servers trên cổng 3000`
   - **VPC:** Chọn `advanced-alb-vpc`
   ![Cấu hình cơ bản](/images/3-VPCSetup/3.2-CreateSecurityGroup/3.2.4-WebSockerServiceSG/01-BasicConfig.png)

3. **Thiết lập Inbound Rules**
   - Nhấp **Add rule** và cấu hình:
     - **Loại:** Custom TCP
     - **Port range:** 3000
     - **Nguồn:** Chọn Security Group `alb-sg` từ danh sách
   ![Cấu hình Inbound Rules](/images/3-VPCSetup/3.2-CreateSecurityGroup/3.2.4-WebSockerServiceSG/02-InboundRule.png)

4. **Hoàn tất**
   - Nhấp **Create security group**