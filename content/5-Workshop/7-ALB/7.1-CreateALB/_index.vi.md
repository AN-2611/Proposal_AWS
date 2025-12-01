+++
title = "Tạo ALB"
date = 2022
weight = 2
chapter = false
pre = "<b>7.1 </b>"
+++
Đầu tiên, điều hướng đến **bảng điều khiển EC2**. Trong menu bên trái, dưới mục **Load Balancing**, nhấp vào **Load Balancers.**
![Bảng điều khiển EC2](/images/7-ALB/7.1-CreateALB/01-EC2Dashboard.png)
1. Nhấp vào nút **Create Load Balancer**.
2. Trong các tùy chọn, tìm Application Load Balancer và nhấp vào Create.
![Bảng điều khiển EC2](/images/7-ALB/7.1-CreateALB/02-ChooseALB.png)
3. Cài đặt cơ bản:
   - **Tên bộ cân bằng tải (Load balancer name):** `advanced-alb`
   - **Lược đồ (Scheme):** Chọn Internet-facing để làm cho nó có thể truy cập từ internet.
   - **Loại địa chỉ IP (IP address type):** Chọn IPv4.
![Cấu hình cơ bản](/images/7-ALB/7.1-CreateALB/03-BasicConfig.png)
4. Thiết lập Ánh xạ mạng (Network Mapping):
   - **VPC:** Chọn **advanced-alb-vpc** của bạn từ menu thả xuống.

   - **Ánh xạ (Mappings):** Trong bảng mạng con (subnets), chọn các hộp kiểm cho hai mạng con công cộng của bạn (**public-subnet-1a** và **public-subnet-1b**). ALB phải nằm trong các mạng con công cộng để có thể truy cập được từ internet.

   - **Nhóm bảo mật (Security groups):** Bỏ chọn nhóm bảo mật mặc định và chọn **alb-sg** mà bạn đã tạo trước đó.
![Tùy chọn mạng](/images/7-ALB/7.1-CreateALB/04-Networking.png)
5. Cấu hình Trình nghe (Listeners) và Định tuyến (Routing):
Phần này định nghĩa cách ALB xử lý lưu lượng truy cập đến trên các cổng khác nhau.
- Trình nghe và định tuyến:
  - Đối với **Hành động mặc định (Default action)**, chọn **web-tg** từ menu thả xuống.
  - Cấu hình chuyển hướng (redirect):
    - **Chuyển hướng đến (Redirect to):** HTTPS
    - **Cổng (Port):** 443
![Tùy chọn mạng](/images/7-ALB/7.1-CreateALB/05-Listen+Routing.png)
6. Chứng chỉ máy chủ SSL/TLS mặc định:
   - **Nguồn chứng chỉ (Certificate source):** Từ ACM
   - **Chứng chỉ (từ ACM):** test.name.vn
   - Chọn **Create load balancer** để hoàn tất.
![Chứng chỉ ACM](/images/7-ALB/7.1-CreateALB/06-ACMCert.png)
7. Quay lại **Load Balancer** bạn đã tạo trước đó. Trong tab **Listeners and rules**, chọn **Add listener**
![Bảng điều khiển ALB](/images/7-ALB/7.1-CreateALB/07-ALBDashBoard.png)
- Trong phần **Hành động mặc định (Default action)**:
   - **Hành động định tuyến (Routing action)**: Chuyển hướng đến URL
   - **Giao thức (Protocol)**: HTTPS
   - **Cổng (Port)**: 443
   - Chọn **Add listener**
![Thêm Trình nghe HTTPS](/images/7-ALB/7.1-CreateALB/08-AddListenerHTTPS.png)
8. Sau khi hoàn tất, bạn sẽ có 2 trình nghe:
   - HTTP:80 → Chuyển hướng đến HTTPS
   - HTTPS:443 → Chuyển tiếp đến **web-tg**
![Kết quả](/images/7-ALB/7.1-CreateALB/09-Result4.png)