---
title : "Tạo và Gắn Internet Gateway (IGW)"
date : "2025-08-18"
weight : 3
chapter : false
pre : " <b> 3.1.2. </b> "
---
#### Tổng quan
Internet Gateway (IGW) là thành phần quan trọng giúp các Public Subnets trong VPC có thể kết nối với Internet. Dưới đây là các bước chi tiết để tạo và gắn IGW vào VPC.

#### Các bước thực hiện

1. **Truy cập VPC Dashboard**
   - Đăng nhập AWS Management Console
   - Tìm kiếm và chọn **VPC** từ thanh tìm kiếm

2. **Bắt đầu tạo Internet Gateway**
   - Trong menu bên trái, chọn **Internet Gateways**
   - Nhấp **Create internet gateway**
   ![VPC Dashboard](/images/3-VPCSetup/3.1-CreateVPC/3.1.2-CreateIGW/01-VPCDashboard.png)

3. **Cấu hình Internet Gateway**
   - **Name tag:** `advanced-alb-igw`
   - Nhấp **Create internet gateway**
   ![VPC Dashboard](/images/3-VPCSetup/3.1-CreateVPC/3.1.2-CreateIGW/02-CreateIGW.png)

4. **Gắn Internet Gateway vào VPC**
   - Chọn IGW vừa tạo
   - Nhấp **Actions**, chọn **Attach to VPC**
   ![VPC Dashboard](/images/3-VPCSetup/3.1-CreateVPC/3.1.2-CreateIGW/03-ActionIGW.png)
   - Chọn VPC `advanced-alb-vpc` từ dropdown và nhấp **Attach internet gateway**
   ![VPC Dashboard](/images/3-VPCSetup/3.1-CreateVPC/3.1.2-CreateIGW/04-AttachIGWtoVPC.png)