+++
title = "Khởi tạo Application Load Balancer"
date = 2022
weight = 8
chapter = false
pre = "<b>7. </b>"
+++

### Giới thiệu
![Biểu tượng Target group](/images/7-ALB/ALB-3.png)
Elastic Load Balancing tự động phân phối lưu lượng truy cập đến của bạn trên nhiều đích, chẳng hạn như các phiên bản EC2, vùng chứa (containers) và địa chỉ IP, trong một hoặc nhiều Vùng sẵn sàng (Availability Zones). Nó giám sát tình trạng của các đích đã đăng ký và chỉ định tuyến lưu lượng truy cập đến các đích khỏe mạnh. Elastic Load Balancing điều chỉnh bộ cân bằng tải của bạn khi lưu lượng truy cập đến thay đổi theo thời gian. Nó có thể tự động mở rộng quy mô để đáp ứng phần lớn khối lượng công việc.

Trong triển khai này, ALB sẽ thực hiện một số chức năng quan trọng:
- **Điểm truy cập công cộng:** Nó cung cấp một tên DNS duy nhất, ổn định để người dùng truy cập ứng dụng của bạn.
- **Phân phối lưu lượng truy cập:** Nó phân phối các yêu cầu đến trên nhiều máy chủ phụ trợ để đảm bảo không có máy chủ nào bị quá tải.
- **Tắt tải SSL/TLS:** Nó xử lý sự phức tạp của việc mã hóa và giải mã lưu lượng HTTPS, giúp các máy chủ phụ trợ của bạn tập trung vào các tác vụ cốt lõi của chúng.
- **Cải thiện bảo mật:** Bằng cách chuyển hướng tất cả lưu lượng HTTP không được mã hóa sang HTTPS được mã hóa, nó đảm bảo giao tiếp an toàn.
- **Giao thức hiện đại:** Nó hỗ trợ nguyên bản HTTP/2, mang lại những cải tiến về hiệu suất như ghép kênh (multiplexing) và nén tiêu đề (header compression).

### Chi phí
- [Giá ALB](https://aws.amazon.com/elasticloadbalancing/pricing/)

### Tài liệu
- [Application Load Balancers](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/application-load-balancers.html)
- [Bật nhật ký truy cập cho Application Load Balancer của bạn](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/enable-access-logging.html)
- [Các phần tử chính sách JSON của AWS: Principal](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_principal.html#principal-services)

### Nội dung
1. [Tạo ALB](7-ALB/7.1-CreateALB)
2. [Bật tính năng Nhật ký truy cập](7-ALB/7.2-EnableAccessLogs)
3. [Cấu hình Quy tắc định tuyến](7-ALB/7.3-ConfigRoutingRules)
4. [Bật Phiên cố định (Sticky Sessions)](7-ALB/7.4-EnableStickySessions)
