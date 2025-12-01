+++
title = "Tạo Auto Scaling Group"
date = 2022
weight = 9
chapter = false
pre = "<b>9.1 </b>"
+++
1. Điều hướng đến bảng điều khiển EC2. Trong menu bên trái, cuộn xuống dưới cùng và nhấp vào **Auto Scaling Groups** (Nhóm tự động thay đổi kích thước). Nhấp vào **Create Auto Scaling group** (Tạo nhóm tự động thay đổi kích thước).
![Bảng điều khiển EC2](/images/9-ASG/9.1-CreateASG/01-EC2Dashboard.png)
1. Trên trang **Choose launch template** (Chọn mẫu khởi chạy):
   - **Auto Scaling group name** (Tên nhóm tự động thay đổi kích thước): `web-service-asg`
   - **Launch template** (Mẫu khởi chạy): `web-service-template`
   - Nhấp vào **Next** (Tiếp theo).
![Tạo ASG dịch vụ web](/images/9-ASG/9.1-CreateASG/02-CreateWebASG.png)
1. Cấu hình Cài đặt mạng:
{{% notice tip %}}
Khởi chạy các phiên bản trong các mạng con riêng là một phương pháp bảo mật tốt nhất, vì chúng không thể được truy cập trực tiếp từ internet.
{{% /notice %}}
   - **VPC:** advanced-alb-vpc
   - **Availability Zones and subnets** (Vùng sẵn sàng và mạng con): private-subnet-1a, private-subnet-1b
   - Nhấp vào **Next** (Tiếp theo).
![Tạo ASG dịch vụ web](/images/9-ASG/9.1-CreateASG/03-NetworkingASG.png)
1. Đính kèm Bộ cân bằng tải:
   - Chọn **Attach to an existing load balancer** (Đính kèm vào bộ cân bằng tải hiện có).
   - Chọn **Choose from your load balancer target groups** (Chọn từ các nhóm mục tiêu của bộ cân bằng tải của bạn).
   - Chọn **web-tg** từ menu thả xuống.
   - Dưới **Health checks** (Kiểm tra tình trạng), giữ nguyên hộp kiểm **Enable ELB health checks** (Bật kiểm tra tình trạng ELB).
   - Nhấp vào **Next** (Tiếp theo).
![Tạo ASG dịch vụ web](/images/9-ASG/9.1-CreateASG/04-LoadBalacingASG.png)
1. Cấu hình Kích thước nhóm và Tự động thay đổi kích thước
   - **Group size** (Kích thước nhóm):
     - **Desired capacity** (Dung lượng mong muốn): 2 (Số lượng phiên bản để bắt đầu).
     - **Minimum capacity** (Dung lượng tối thiểu): 1 (Kích thước nhỏ nhất của nhóm).
     - **Maximum capacity** (Dung lượng tối đa): 4 (Kích thước lớn nhất của nhóm).
   - **Scaling policies** (Chính sách tự động thay đổi kích thước):
     - Chọn **Target tracking scaling policy** (Chính sách tự động thay đổi kích thước theo dõi mục tiêu).
     - **Metric type** (Loại chỉ số): Average CPU utilization (Mức sử dụng CPU trung bình).
     - **Target value** (Giá trị mục tiêu): 70 %.
     - Giữ nguyên các khoảng thời gian chờ mặc định. Chính sách này sẽ tự động thêm các phiên bản nếu tải CPU trung bình trên toàn bộ nhóm tăng lên trên 70%.
![Tạo ASG dịch vụ web](/images/9-ASG/9.1-CreateASG/05-ScalingPolicy.png)
1. Thêm Thẻ:
    - **Key** (Khóa): Name
    - **Value** (Giá trị): web-server
    - Đảm bảo "Tag new instances" (Gắn thẻ các phiên bản mới) được chọn.
    - Nhấp vào **Next** (Tiếp theo).

![Tạo ASG dịch vụ web](/images/9-ASG/9.1-CreateASG/06-Tags.png)

7. Xem lại và Tạo:
      - Cẩn thận xem lại tất cả các cài đặt trên trang cuối cùng.
      - Nhấp vào **Create Auto Scaling group** (Tạo nhóm tự động thay đổi kích thước). ASG bây giờ sẽ bắt đầu khởi chạy hai phiên bản **web-server** mong muốn của bạn.
8. Tạo ASG cho API và WebSocket:
Bây giờ, lặp lại quy trình để tạo hai ASG còn lại. Các bước giống hệt nhau; bạn chỉ cần thay đổi **Name** (Tên), **Launch Template** (Mẫu khởi chạy) và **Target Group** (Nhóm mục tiêu) cho mỗi ASG.
### Đối với ASG Dịch vụ API:
   - **Auto Scaling group name:** `api-service-asg`
   - **Launch template:** api-service-template
   - **Target group:** api-tg
   - Giữ nguyên tất cả các cài đặt khác: mạng con riêng, Desired=2/Min=1/Max=4, mở rộng CPU ở 70%, v.v.

### Đối với ASG Dịch vụ WebSocket:
   - **Auto Scaling group name:** `websocket-service-asg`
   - **Launch template:** websocket-service-template
   - **Target group:** websocket-tg
   - Giữ nguyên tất cả các cài đặt khác.
![Sau khi tạo 3 ASG](/images/9-ASG/9.1-CreateASG/07-ResultASG.png)
