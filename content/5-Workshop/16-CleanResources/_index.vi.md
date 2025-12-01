
+++
title = "Dọn dẹp tài nguyên"
date = 2022
weight = 17
chapter = false
pre = "<b>16. </b>"
+++
1. Đi tới **VPC > Internet gateways**. Chọn **Detach from VPC** (Tách khỏi VPC)
![Xóa IGW ](/images/16-CleanResources/01-IGW.png)
2. Cuộn xuống **NAT Gateways**. Chọn **Delete NAT Gateway** (Xóa Cổng NAT)
![Xóa IGW ](/images/16-CleanResources/02-NAT.png)
3. Đi tới **Subnets**. Đánh dấu vào ô cho tất cả các mạng con. Chọn **Delete subnets** (Xóa mạng con)
![Xóa IGW ](/images/16-CleanResources/03-Subnet.png)
4. Đi tới **Route tables**. Đánh dấu vào ô cho **public-rt** và **private-rt**. Chọn **Delete route tables** (Xóa bảng định tuyến)
![Xóa IGW ](/images/16-CleanResources/04-RT.png)
5. Đi tới **VPC**. Đánh dấu vào ô cho **advanced-alb-vpc**. Chọn **Delete VPC** (Xóa VPC)
![Xóa IGW ](/images/16-CleanResources/05-VPC.png)
6. Đi tới **Security groups**. Đánh dấu vào ô cho các nhóm bảo mật. Chọn **Delete security groups** (Xóa nhóm bảo mật)
![Xóa IGW ](/images/16-CleanResources/06-SG.png)
7. Điều hướng đến Bảng điều khiển EC2, cuộn xuống **Auto Scaling Groups**. Đánh dấu vào ô cho ba ASG. Chọn **Delete** (Xóa)
![Xóa IGW ](/images/16-CleanResources/07-ASG.png)
8. Tiếp tục cuộn xuống **Load Balancer**. Đánh dấu vào ô cho **advanced-alb**. Chọn **Delete load balancer** (Xóa bộ cân bằng tải)
![Xóa IGW ](/images/16-CleanResources/08-LBC.png)
9. Trong menu **Load balancing**. Chọn **Target groups**. Đánh dấu vào ô cho cả ba nhóm đích. Chọn **Delete** (Xóa)
![Xóa IGW ](/images/16-CleanResources/09-TG-2.png)
10. Trong menu **Network & Security**. Chọn **Elastic IPs**. Đánh dấu vào ô và sau đó chọn **Release Elastic IP addresses** (Giải phóng địa chỉ IP động)
![Xóa IGW ](/images/16-CleanResources/10-ElasticIP.png)
11. Điều hướng đến **SNS Dashboard** > **Topics**. Chọn **Delete** (Xóa)
![Xóa IGW ](/images/16-CleanResources/11-SNS.png)
12. Điều hướng đến **CloudWatch Dashboard** > **All alarms**. Đánh dấu vào tất cả các ô. Chọn **Delete** (Xóa)
![Xóa IGW ](/images/16-CleanResources/12-CW.png)
13. Điều hướng đến **Billing and Cost Management** > **Budgets** > **Overview**. Chọn **Delete** (Xóa)
![Xóa IGW ](/images/16-CleanResources/13-Cost.png)
14. Điều hướng đến **Route 53** > **Hosted zones**. Đánh dấu vào ô. Chọn **Delete** (Xóa)
![Xóa IGW ](/images/16-CleanResources/14-53.png)
15. Điều hướng đến **AWS Certificate Manager Certificates** > **Certificates**. Trong menu **More actions** (Thao tác khác), chọn **Delete** (Xóa)
![Xóa IGW ](/images/16-CleanResources/15-cert.png)
