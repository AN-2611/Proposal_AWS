+++
title = "Bật tính năng Nhật ký truy cập"
date = 2022
weight = 3
chapter = false
pre = "<b>7.2 </b>"
+++
1. Quay lại chi tiết Load Balancer: **advanced-alb**. Chọn **Actions** sau đó nhấp vào **Edit load balancer attributes**
![Bảng điều khiển EC2](/images/7-ALB/7.2-EnableAccessLogs/01-ALBDashboard.png)
2. Trong trang **Edit load balancer attributes**:
   - Cuộn xuống để bật **Access logs** (Nhật ký truy cập)
   - Chọn **Browse S3** để tìm S3 bucket bạn đã tạo ở các bước trước
![Bảng điều khiển EC2](/images/7-ALB/7.2-EnableAccessLogs/02-EnableAccessLogs.png)
