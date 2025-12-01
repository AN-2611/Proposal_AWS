---
title : "Tạo Security Groups"
date : "2025-10-10"
weight : 2
chapter : false
pre : " <b> 3.2 </b> "
---

### Tổng quan về Security Groups
Security Groups hoạt động như một tường lửa ảo có trạng thái, kiểm soát tất cả lưu lượng mạng vào và ra khỏi các tài nguyên của bạn. Cấu hình dưới đây triển khai mô hình bảo mật nhiều lớp, một phương pháp tốt nhất trong thực tế.

#### Nguyên tắc cơ bản
1. **Nguyên tắc Ít Đặc quyền Nhất (Principle of Least Privilege):** Chỉ mở các cổng cần thiết. Application Load Balancer (ALB) là thành phần duy nhất được tiếp xúc với Internet.
2. **Backend An toàn:** Các dịch vụ backend (Web, API, WebSocket) được cách ly hoàn toàn khỏi Internet công cộng. Chúng được cấu hình chỉ chấp nhận lưu lượng bắt nguồn từ Security Group của ALB. Điều này đảm bảo tất cả các yêu cầu được định tuyến và kiểm tra bởi Load Balancer trước khi đến mã ứng dụng của bạn.

### Nội dung chi tiết
1. **[Tạo Security Group cho ALB](/3-VPCSetup/3.2-CreateSecurityGroup/3.2.1-ALBSG)**
   - **Mục đích:** Cho phép lưu lượng HTTP/HTTPS từ Internet đến ALB.
   - **Cổng mở:** 80 (HTTP), 443 (HTTPS)
   - **Nguồn:** 0.0.0.0/0 (Internet)

2. **[Tạo Security Group cho WebService](/3-VPCSetup/3.2-CreateSecurityGroup/3.2.2-WebServiceSG)**
   - **Mục đích:** Cho phép lưu lượng từ ALB đến các instance WebService.
   - **Cổng mở:** 80 (HTTP)
   - **Nguồn:** Security Group của ALB

3. **[Tạo Security Group cho APIService](/3-VPCSetup/3.2-CreateSecurityGroup/3.2.3-APIServiceSG)**
   - **Mục đích:** Cho phép lưu lượng từ ALB đến các instance APIService.
   - **Cổng mở:** 8080 (API)
   - **Nguồn:** Security Group của ALB

4. **[Tạo Security Group cho WebSocketService](/3-VPCSetup/3.2-CreateSecurityGroup/3.2.4-WebSockerServiceSG)**
   - **Mục đích:** Cho phép lưu lượng từ ALB đến các instance WebSocketService.
   - **Cổng mở:** 3000 (WebSocket)
   - **Nguồn:** Security Group của ALB