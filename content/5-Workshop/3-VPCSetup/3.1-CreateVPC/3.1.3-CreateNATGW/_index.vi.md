---
title : "Tạo NAT Gateway"
date : "2025-10-10"
weight : 4
chapter : false
pre : " <b> 3.1.3. </b> "
---


#### Tổng quan
NAT Gateway cho phép các instance trong Private Subnets khởi tạo lưu lượng ra Internet mà vẫn giữ được tính riêng tư. Dưới đây là các bước chi tiết để tạo và cấu hình NAT Gateway.

#### Các bước thực hiện

1. **Truy cập VPC Dashboard**
   - Đăng nhập AWS Management Console
   - Tìm kiếm và chọn **VPC** từ thanh tìm kiếm

2. **Bắt đầu tạo NAT Gateway**
   - Trong menu bên trái, chọn **NAT Gateways**
   - Nhấp **Create NAT gateway**
   ![VPC Dashboard](/images/3-VPCSetup/3.1-CreateVPC/3.1.3-CreateNATGW/01-VPCDashboard.png)

3. **Cấu hình NAT Gateway**
   - **Name:** `advanced-alb-nat`
   - **Subnet:** `public-subnet-1a`
   - **Connectivity type:** Public
   - **Elastic IP allocation ID:** Nhấp **Allocate Elastic IP**. Điều này sẽ tạo và liên kết một địa chỉ IP công cộng tĩnh mới cho NAT Gateway.
   - Nhấp **Create NAT gateway**
   ![Configure NAT Gateway](/images/3-VPCSetup/3.1-CreateVPC/3.1.3-CreateNATGW/02-ConfigureNATGW.png)