---
title : "Workshop"
date :  "2025-10-10"
weight : 5
chapter : false
pre: " <b> 5. </b> "
---
# TRIỂN KHAI CÁC TÍNH NĂNG NÂNG CAO CỦA AWS APPLICATION LOAD BALANCER

### Tổng quan
Bài thực hành này cung cấp một hướng dẫn toàn diện, thực tế về việc triển khai và quản lý các khả năng nâng cao của AWS Application Load Balancer (ALB). Người tham gia sẽ vượt ra ngoài cân bằng tải cơ bản để cấu hình một giải pháp phân phối ứng dụng có tính sẵn sàng cao, hiệu suất tốt và thông minh. Bằng cách thực hiện các kịch bản thực tế, bạn sẽ học cách tận dụng các tính năng quan trọng cho các ứng dụng hiện đại, có khả năng mở rộng và bền vững, bao gồm định tuyến phức tạp, hỗ trợ giao thức và các phương pháp hay nhất trong vận hành.

![ConnectPrivate](/images/arc.jpeg)
### Quy trình làm việc
#### Giai đoạn 1: Thiết lập Mạng Cơ bản (VPC)
Giai đoạn này thiết lập môi trường mạng cô lập cho ứng dụng.

*   **Tạo VPC:** Một VPC được tạo với khối CIDR `10.0.0.0/16`.

*   **Tạo Subnet:** Bốn subnet được tạo trên hai Vùng sẵn sàng (Availability Zone) để đảm bảo tính sẵn sàng cao:
    *   `public-subnet-1a` (`10.0.1.0/24`)
    *   `public-subnet-1b` (`10.0.2.0/24`)
    *   `private-subnet-1a` (`10.0.3.0/24`)
    *   `private-subnet-1b` (`10.0.4.0/24`)

*   **Cấu hình Gateway:** Một Internet Gateway được gắn vào VPC để truy cập internet công cộng, và một NAT Gateway được đặt trong một subnet công cộng để cho phép các instance riêng tư truy cập internet.

*   **Thiết lập Bảng Định tuyến (Route Table):** Một bảng định tuyến công cộng được cấu hình để định tuyến lưu lượng truy cập qua Internet Gateway, và một bảng định tuyến riêng tư được thiết lập để định tuyến lưu lượng truy cập đi từ các subnet riêng tư qua NAT Gateway.

#### Giai đoạn 2: Bảo mật & Cấu hình
Giai đoạn này tập trung vào việc bảo mật môi trường và chuẩn bị cho việc triển khai.

*   **Tạo Nhóm Bảo mật (Security Group):** Các nhóm bảo mật phân lớp được tạo để kiểm soát luồng lưu lượng truy cập:
    *   `alb-sg`: Cho phép lưu lượng HTTP (80) và HTTPS (443) công cộng.
    *   `web-sg`: Chỉ cho phép lưu lượng truy cập từ `alb-sg` trên cổng 80.
    *   `api-sg`: Chỉ cho phép lưu lượng truy cập từ `alb-sg` trên cổng 8080.
    *   `websocket-sg`: Chỉ cho phép lưu lượng truy cập từ `alb-sg` trên cổng 3000.

*   **Yêu cầu Chứng chỉ SSL:** Một chứng chỉ SSL cho tên miền đã được yêu cầu và xác thực bằng AWS Certificate Manager (ACM) để kích hoạt HTTPS.

*   **Tạo Vai trò IAM (IAM Role):** Một vai trò IAM (`ec2-alb-role`) đã được tạo cho các instance EC2, cấp cho chúng quyền tương tác với CloudWatch, S3 và SNS mà không cần lưu trữ thông tin xác thực.

*   **Tạo S3 Bucket:** Một S3 bucket đã được tạo để lưu trữ nhật ký truy cập của ALB cho mục đích kiểm toán và phân tích.

#### Giai đoạn 3: Lớp Ứng dụng & Tính toán
Giai đoạn này triển khai các thành phần cốt lõi của ứng dụng.

*   **Tạo Nhóm Đích (Target Group):** Ba nhóm đích riêng biệt đã được tạo để định tuyến lưu lượng truy cập đến các microservice khác nhau, mỗi nhóm có một đường dẫn kiểm tra tình trạng (health check path) cụ thể:
    *   `web-tg` (Cổng 80, `/`)
    *   `api-tg` (Cổng 8080, `/api/health`)
    *   `websocket-tg` (Cổng 3000, `/ws/health`)

*   **Tạo Bộ Cân bằng Tải Ứng dụng (Application Load Balancer - ALB):** Một ALB hướng internet đã được tạo trong các subnet công cộng, được cấu hình với nhóm bảo mật `alb-sg` và chứng chỉ ACM. Các Listener đã được thiết lập để chuyển hướng HTTP sang HTTPS và xử lý định tuyến dựa trên nội dung.

*   **Kích hoạt các Tính năng Nâng cao của ALB:**
    *   **Sticky Sessions:** Được kích hoạt trên `web-tg` để duy trì phiên.
    *   **Access Logs:** Được cấu hình để gửi nhật ký đến S3 bucket.

*   **Tạo Mẫu Khởi chạy (Launch Template):** Ba mẫu khởi chạy riêng biệt đã được tạo, mỗi mẫu có một tập lệnh dữ liệu người dùng (user data script) cụ thể để khởi động ứng dụng:
    *   `web-service-template` (NGINX)
    *   `api-service-template` (Node.js/Express)
    *   `websocket-service-template` (Node.js/WebSocket)

*   **Tạo Nhóm Tự động Mở rộng (Auto Scaling Group - ASG):** Ba Nhóm Tự động Mở rộng đã được khởi chạy trong các subnet riêng tư, mỗi nhóm được liên kết với Mẫu Khởi chạy và Nhóm Đích tương ứng, được cấu hình để duy trì số lượng mong muốn là 2 instance và tự động mở rộng dựa trên mức sử dụng CPU.

#### Giai đoạn 4: Giám sát, DNS & Quản lý Chi phí
Giai đoạn cuối cùng này giúp ứng dụng có thể quan sát được, truy cập công khai và được giám sát về tài chính.

*   **Cấu hình Giám sát:**
    *   Một Chủ đề SNS (SNS Topic) (`alb-alerts`) đã được tạo để nhận thông báo.
    *   Các cảnh báo CloudWatch (CloudWatch Alarms) đã được đặt cho các chỉ số quan trọng như `RequestCountPerTarget` và `CPUUtilization` để gửi cảnh báo đến chủ đề SNS.
    *   Một Bảng điều khiển CloudWatch (CloudWatch Dashboard) đã được xây dựng để trực quan hóa tình trạng của ALB, Nhóm Đích và các instance EC2 theo thời gian thực.

*   **Cấu hình DNS:** Amazon Route 53 đã được sử dụng để tạo một bản ghi A, trỏ tên miền gốc đến ALB, và bản ghi CNAME định tuyến lưu lượng truy cập đến tên miền phụ, giúp ứng dụng có thể truy cập được qua một URL thân thiện.

*   **Thiết lập Giám sát Chi phí:** AWS Cost Explorer đã được kích hoạt, và một Ngân sách AWS (AWS Budget) đã được tạo để giám sát chi tiêu hàng tháng và gửi cảnh báo nếu chi phí tiếp cận giới hạn đã định.

### Nội dung
 1. [Giới thiệu ](1-Introduce)
 2. [Chuẩn bị](2-Preparation/)
 3. [Cơ sở hạ tầng mạng](3-VPCSetup)
 4. [Yêu cầu Chứng chỉ SSL](4-ACM)
 5. [Khởi tạo S3 Bucket](5-S3Bucket)
 6. [Tạo Nhóm Đích](6-TargetGroup)
 7. [Khởi tạo Application Load Balancer](7-ALB)
 8. [Khởi tạo Mẫu Khởi chạy EC2](8-EC2LaunchTemplates)
 9. [ Khởi tạo Nhóm Tự động Mở rộng](9-ASG)
 10. [Tạo chủ đề SNS](10-SNS)
 11. [Khởi tạo Cảnh báo CloudWatch](11-CW)
 12. [ Khởi tạo Giám sát Chi phí](12-Cost)
 13. [Cấu hình DNS](13-ConfigDNS)
 14. [Kiểm tra kết quả](14-CheckResult)
 15. [ Kiểm thử Hiệu suất](15-PerformanceTesting)
 16. [ Dọn dẹp Tài nguyên](16-CleanResources)
