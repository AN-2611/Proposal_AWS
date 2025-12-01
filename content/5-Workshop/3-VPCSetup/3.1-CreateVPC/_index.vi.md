---
title : "Thiết lập VPC"
date : "2025-10-10"
weight : 1
chapter : false
pre : " <b> 3.1. </b> "
---

### Hướng dẫn chi tiết tạo và cấu hình VPC trên AWS

1. **Truy cập dịch vụ VPC**
   - Trên thanh tìm kiếm AWS, nhập `VPC` và chọn **VPC** từ kết quả hiển thị
   ![Find VPC](/images/3-VPCSetup/3.1-CreateVPC/01-FindVPC.png)

2. **Bắt đầu tạo VPC mới**
   - Tại trang VPC Dashboard, nhấp **Create VPC**
   ![VPC Dashboard](/images/3-VPCSetup/3.1-CreateVPC/02-VPCDashboard.png)

3. **Cấu hình thông số VPC**
   - **Resources to create:** Chọn "VPC only"
   - **Name tag:** `advanced-alb-vpc`
   - **IPv4 CIDR block:** `10.0.0.0/16` (dải mạng riêng lớn cho phép tạo nhiều subnet)
   ![Create VPC](/images/3-VPCSetup/3.1-CreateVPC/03-CreateVPC.png)

4. **Chỉnh sửa cài đặt VPC sau khi tạo**
   - Chọn VPC vừa tạo từ danh sách
   - Nhấp **Actions** > **Edit VPC settings**
   ![Edit VPC Setting](/images/3-VPCSetup/3.1-CreateVPC/04-EditVPCSettings.png)

5. **Bật tính năng DNS quan trọng**
   - Tick chọn **Enable DNS hostnames**
   - Đảm bảo **Enable DNS resolution** cũng được chọn
   - Nhấp **Save** để lưu thay đổi
   ![DNS resol in VPC Setting](/images/3-VPCSetup/3.1-CreateVPC/05-EnableDNSResolution.png)