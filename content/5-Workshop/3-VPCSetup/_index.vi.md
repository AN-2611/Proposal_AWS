---
title : "Cơ sở hạ tầng mạng"
date : "2025-10-10"
weight : 4
chapter : false
pre : " <b> 3. </b> "
---
Trong bài thực hành này, bạn sẽ làm việc trong một Virtual Private Cloud (VPC) đã được cấu hình sẵn. Thiết lập này cung cấp nền tảng mạng cần thiết cho ứng dụng và bộ cân bằng tải của chúng ta.

#### Môi trường bao gồm:

  - Một VPC với dải địa chỉ IP tùy chỉnh.
  - Các Security Group (Nhóm bảo mật) hoạt động như tường lửa ảo, được cấu hình để cho phép lưu lượng truy cập web công khai đến ALB và sau đó hạn chế quyền truy cập vào các máy chủ ứng dụng của chúng ta (các EC2 instance).
  - Hai Subnet công khai (Public Subnet) và hai Subnet riêng tư (Private Subnet), được phân bổ trên hai Vùng sẵn sàng (Availability Zone) khác nhau để đảm bảo tính sẵn sàng cao.
  - Cấu hình các Bảng định tuyến (Route Table) để hướng lưu lượng truy cập từ các subnet công khai đến Internet Gateway và từ các subnet riêng tư đến NAT Gateway.
  - Một Internet Gateway được đính kèm vào VPC để cho phép giao tiếp với internet.
  - Sử dụng AWS Certificate Manager (ACM) để yêu cầu và xác thực chứng chỉ SSL/TLS công khai cho miền của chúng ta.

#### Chi phí:

1.  [NAT Gateway:](https://aws.amazon.com/vi/vpc/pricing/) $0.045 mỗi giờ.
2.  [Địa chỉ IPv4 công khai (Public IPv4 Address):](https://aws.amazon.com/vi/vpc/pricing/) $0.005 mỗi giờ.

#### Tài liệu tham khảo:

1.  [Tài liệu về VPC](https://docs.aws.amazon.com/vpc/)
2.  [Tài liệu về NAT Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html)
3.  [Tài liệu về Internet Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html)
4.  [Tài liệu về Route Table](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html)
5.  [Tài liệu về Security group](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html)

### Nội dung

1.  [Thiết lập VPC](https://www.google.com/search?q=3.1-CreateVPC/)
2.  [Tạo Security group](https://www.google.com/search?q=3.2-CreateSecurityGroup/)