
+++
title = "Tạo Target Groups"
date = 2022
weight = 6
chapter = false
pre = "<b>6.1 </b>"
+++

1. Đầu tiên, điều hướng đến **bảng điều khiển EC2**. Trong menu bên trái, cuộn xuống **Load Balancing** và nhấp vào **Target Groups.**
![Bảng điều khiển EC2](/images/6-TargetGroup/6.1-WebTG/01-EC2Dashboard.png)

2. **Chọn loại đích (target type):** Chọn **Instances**.
- Cấu hình cơ bản:
    - **Tên nhóm đích (Target group name):** `web-tg`
    - **Giao thức / Cổng (Protocol / Port):** HTTP / 80
    - **VPC:** **alb-advanced-vpc**
    - **Phiên bản giao thức (Protocol version):** HTTP1
![Cấu hình cơ bản](/images/6-TargetGroup/6.1-WebTG/02-BasicConfig.png)

- Kiểm tra sức khỏe (Health checks):
    - **Giao thức kiểm tra sức khỏe (Health check protocol):** HTTP
    - **Đường dẫn kiểm tra sức khỏe (Health check path):** /
    - Nhấp vào **Cài đặt kiểm tra sức khỏe nâng cao (Advanced health check settings):**
      - **Ngưỡng khỏe mạnh (Healthy threshold):** 2 (Một phiên bản được coi là khỏe mạnh sau 2 lần kiểm tra thành công liên tiếp).
      - **Khoảng thời gian (Interval):** 15 giây (Thời gian giữa các lần kiểm tra).
![Kiểm tra sức khỏe](/images/6-TargetGroup/6.1-WebTG/03-HealthCheck-1.png)

3. Nhấp vào **Next**. Trên trang Đăng ký đích (Register targets), hiện tại không chọn bất kỳ phiên bản nào. Chúng ta sẽ khởi chạy và đăng ký chúng sau.

4. Nhấp vào **Create target group.**

5. Lặp lại quá trình tạo ở trên cho hai nhóm đích còn lại, sử dụng các cài đặt cụ thể dưới đây. Tất cả các cài đặt khác (như VPC, loại đích và kiểm tra sức khỏe nâng cao) có thể giữ nguyên.
   - Nhóm đích API (`api-tg`):
        - **Tên nhóm đích:** api-tg
        - **Cổng:** 8080
        - **Đường dẫn kiểm tra sức khỏe:** /api/health
   - Nhóm đích WebSocket (`websocket-tg`):
        - **Tên nhóm đích:** websocket-tg
        - **Cổng:** 3000
        - **Đường dẫn kiểm tra sức khỏe:** /ws/health

6. Sau khi hoàn tất, bạn sẽ có 3 nhóm đích:
![Kết quả cuối cùng](/images/6-TargetGroup/6.1-WebTG/04-Result.png)
