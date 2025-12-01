---
title : "Tạo và Cấu hình Route Tables"
date : "2025-08-18"
weight : 5
chapter : false
pre : " <b> 3.1.4 </b> "
---

#### Tổng quan
Route Tables là thành phần quan trọng giúp định tuyến lưu lượng mạng từ các Subnets trong VPC đến các đích đến khác nhau như Internet Gateway hoặc NAT Gateway. Dưới đây là các bước chi tiết để tạo và cấu hình Route Tables cho Public và Private Subnets.

#### Các bước thực hiện

1. **Truy cập VPC Dashboard**
   - Đăng nhập AWS Management Console
   - Tìm kiếm và chọn **VPC** từ thanh tìm kiếm

2. **Tạo Route Table cho Public Subnets**
   - Trong menu bên trái, chọn **Route Tables**
   - Nhấp **Create route table**
   - **Name:** `public-rt`
   - **VPC:** Chọn `advanced-alb-vpc`
   - Nhấp **Create route table**
   ![VPC Dashboard](/images/3-VPCSetup/3.1-CreateVPC/3.1.4-CreateRouteTable/01-ConfigRT.png)

3. **Cấu hình Routes cho Public Route Table**
   - Trong phần chi tiết, chọn tab **Routes** và nhấp **Edit routes**
   ![Configure route](/images/3-VPCSetup/3.1-CreateVPC/3.1.4-CreateRouteTable/02-EditRoute.png)
   - Nhấp **Add route**
   - **Destination:** 0.0.0.0/0
   - **Target:** Chọn Internet Gateway, sau đó chọn `advanced-alb-igw`
   - Nhấp **Save changes**
   ![Add route](/images/3-VPCSetup/3.1-CreateVPC/3.1.4-CreateRouteTable/03-AddRoute.png)

4. **Liên kết Public Subnets với Public Route Table**
   - Chọn tab **Subnet associations** và nhấp **Edit subnet associations**
   ![Configure route](/images/3-VPCSetup/3.1-CreateVPC/3.1.4-CreateRouteTable/04-SubnetAssociation.png)
   - Chọn hai Public Subnets `public-subnet-1a` và `public-subnet-1b`
   - Nhấp **Save associations**
   ![Add route](/images/3-VPCSetup/3.1-CreateVPC/3.1.4-CreateRouteTable/05-EditSubnetAssociate.png)

5. **Tạo Route Table cho Private Subnets**
   - Quay lại **Route Tables** và nhấp **Create route table**
   - **Name:** `private-rt`
   - **VPC:** `advanced-alb-vpc`
   - Nhấp **Create route table**
   ![Add route](/images/3-VPCSetup/3.1-CreateVPC/3.1.4-CreateRouteTable/06-ConfigPrivateRT.png)

6. **Cấu hình Routes cho Private Route Table**
   - Trong phần chi tiết, chọn tab **Routes** và nhấp **Edit routes**
   ![Add route](/images/3-VPCSetup/3.1-CreateVPC/3.1.4-CreateRouteTable/07-EditPrivateRT.png)
   - Nhấp **Add routes**
   - **Destination:** 0.0.0.0/0
   - **Target:** Chọn NAT Gateway, sau đó chọn `advanced-alb-nat`
   - Nhấp **Save changes**

7. **Liên kết Private Subnets với Private Route Table**
   - Chọn tab **Subnet associations** và nhấp **Edit subnet associations**
   ![Add route](/images/3-VPCSetup/3.1-CreateVPC/3.1.4-CreateRouteTable/08-PrivateRTAssociate.png)
   - Chọn hai Private Subnets `private-subnet-1a` và `private-subnet-1b`
   - Nhấp **Save associations**
   ![Edit RT associate](/images/3-VPCSetup/3.1-CreateVPC/3.1.4-CreateRouteTable/09-EditPrivateRTAssociate.png)
