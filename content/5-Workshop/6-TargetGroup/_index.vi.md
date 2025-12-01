+++
title = "Tạo Target Groups"
date = 2022
weight = 7
chapter = false
pre = "<b>6. </b>"
+++

### Giới thiệu
![Biểu tượng Target group](/images/6-TargetGroup/icon.png)
Target Group là một nhóm logic các tài nguyên đích, chẳng hạn như các phiên bản EC2, sẽ xử lý các yêu cầu. Application Load Balancer (ALB) không gửi lưu lượng truy cập trực tiếp đến các phiên bản; thay vào đó, nó định tuyến lưu lượng truy cập đến một nhóm đích (target group), sau đó nhóm này sẽ phân phối lưu lượng truy cập cho các phiên bản đã đăng ký của nó.

Mỗi nhóm đích được cấu hình với một giao thức và số cổng cụ thể. Quan trọng hơn, nó bao gồm cấu hình kiểm tra sức khỏe (health check). ALB sử dụng kiểm tra sức khỏe này để liên tục giám sát trạng thái của từng phiên bản trong nhóm. Nếu một phiên bản không vượt qua kiểm tra sức khỏe, ALB sẽ ngừng gửi lưu lượng truy cập đến đó và chuyển hướng các yêu cầu đến các phiên bản khỏe mạnh còn lại, đảm bảo tính sẵn sàng cao và khả năng chịu lỗi cho ứng dụng của bạn.

### Tài liệu
- [Nhóm đích cho Application Load Balancer của bạn](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-target-groups.html)
