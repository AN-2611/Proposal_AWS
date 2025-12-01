---
title : "Tạo Subnets"
date : "2025-08-18"
weight : 2
chapter : false
pre : " <b> 3.1.1. </b> "
---
#### Tổng quan
Chúng ta sẽ tạo **hai Public Subnets** và **hai Private Subnets** trải đều trên **hai Availability Zones (AZs)** để đảm bảo tính sẵn sàng cao và phân tán tải.

#### Các bước thực hiện

1. **Truy cập VPC Dashboard**
   - Đăng nhập AWS Management Console
   - Tìm kiếm và chọn **VPC** từ thanh tìm kiếm

2. **Bắt đầu tạo Subnet**
   - Trong menu bên trái, chọn **Subnets**
   - Nhấp **Create subnet**
   ![VPC Dashboard](/images/3-VPCSetup/3.1-CreateVPC/3.1.1-CreateSubnet/01-SubnetDashboard.png)

3. **Chọn VPC**
   - Chọn VPC bạn vừa tạo (ví dụ: `advanced-alb-vpc`)

4. **Cấu hình các Subnets**
   Tạo lần lượt 4 Subnets với các thông số sau:

   - **Subnet 1 (Public)**
     - **Subnet name:** `public-subnet-1a`
     - **Availability Zone:** `us-east-1a`
     - **IPv4 CIDR block:** `10.0.1.0/24`
     - Nhấp **Add new subnet** để tiếp tục

   - **Subnet 2 (Public)**
     - **Subnet name:** `public-subnet-1b`
     - **Availability Zone:** `us-east-1b`
     - **IPv4 CIDR block:** `10.0.2.0/24`

   - **Subnet 3 (Private)**
     - **Subnet name:** `private-subnet-1a`
     - **Availability Zone:** `us-east-1a`
     - **IPv4 CIDR block:** `10.0.3.0/24`

   - **Subnet 4 (Private)**
     - **Subnet name:** `private-subnet-1b`
     - **Availability Zone:** `us-east-1b`
     - **IPv4 CIDR block:** `10.0.4.0/24`

5. **Hoàn tất quá trình**
   - Sau khi định nghĩa xong cả 4 Subnets, nhấp **Create subnet**
   ![Create Subnet Success](/images/3-VPCSetup/3.1-CreateVPC/3.1.1-CreateSubnet/02-CreateSuccess.png)
