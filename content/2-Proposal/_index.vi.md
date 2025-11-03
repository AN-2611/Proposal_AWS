---
title: "Bản đề xuất"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 1. </b> "
---


# AWS APPLICATION LOAD BALANCER
## TRIỂN KHAI CÁC TÍNH NĂNG NÂNG CAO CỦA AWS APPLICATION LOAD BALANCER 

![ALB](/images/arc.jpeg)

### 1. Tóm tắt điều hành  
Báo cáo này trình bày đánh giá và đề xuất triển khai một kiến trúc hệ thống web có độ sẵn sàng cao và bảo mật tốt trên nền tảng AWS, được triển khai tại khu vực us-east-1. Kiến trúc bao gồm các thành phần: Route 53, Certificate Manager (ACM), Application Load Balancer (ALB), nhóm Auto Scaling, CloudWatch, S3 và các máy chủ EC2 chạy trong private subnet trên hai Availability Zone.

Mục tiêu của kiến trúc là xây dựng một hệ thống ổn định, dễ mở rộng, tiết kiệm chi phí và đảm bảo an toàn, phục vụ cho các dịch vụ Web, API và WebSocket trong môi trường sản xuất.

### 2. Tuyên bố vấn đề
#### *Vấn đề hiện tại*  
Trong nhiều hệ thống web truyền thống hoặc hạ tầng on-premises, thường tồn tại các vấn đề sau:

- Chi phí đầu tư và bảo trì cao: Việc đầu tư phần cứng, thiết bị lưu trữ, hệ thống mạng và nguồn nhân lực kỹ thuật yêu cầu chi phí ban đầu lớn. Ngoài ra, chi phí bảo trì, nâng cấp và thay thế định kỳ khiến tổng chi phí sở hữu (TCO) tăng cao.

- Khi lưu lượng truy cập tăng đột biến, việc mở rộng hạ tầng phải thực hiện thủ công, mất nhiều thời gian và có thể gây gián đoạn dịch vụ. Nhiều hệ thống phải đầu tư dư thừa tài nguyên để phòng ngừa, dẫn đến lãng phí công suất.

- Khả năng chịu lỗi thấp: Một sự cố phần cứng, lỗi cấu hình hoặc mất điện có thể làm gián đoạn toàn bộ hệ thống backend. Cơ chế dự phòng và tự động phục hồi thường khó triển khai trên hạ tầng vật lý truyền thống.

- Khó giám sát và khắc phục sự cố: Hệ thống on-premises thường thiếu công cụ quan sát và giám sát tập trung. Việc phát hiện sự cố, theo dõi hiệu năng hoặc phân tích log đòi hỏi thao tác thủ công, làm chậm quá trình phản ứng và khắc phục.

- Gánh nặng bảo mật và tuân thủ: Việc duy trì tường lửa, quản lý bản vá bảo mật, kiểm soát truy cập và sao lưu dữ liệu phải thực hiện thủ công, dễ sai sót và tiêu tốn nguồn lực vận hành.

Những hạn chế này khiến chu trình phát triển phần mềm chậm, chi phí vận hành cao, độ tin cậy thấp, và thiếu tính linh hoạt cần thiết để đáp ứng nhu cầu thay đổi nhanh của các ứng dụng web hiện đại.

#### *Giải pháp*  

Giải pháp được đề xuất là triển khai ứng dụng web theo kiến trúc ba tầng (3-tier) trên AWS, gồm:
- Lớp trình bày (Presentation Layer): Người dùng truy cập thông qua Route 53 và ALB qua giao thức HTTPS (được cấp chứng chỉ bởi ACM).
- Lớp ứng dụng (Application Layer): Chạy trên các EC2 instances trong private subnet, chia thành ba nhóm dịch vụ độc lập: web, API, và WebSocket.
- Lớp dữ liệu và giám sát (Data & Monitoring Layer): Lưu trữ log trên S3, giám sát tài nguyên bằng CloudWatch, cảnh báo qua SNS.

Các Auto Scaling Groups đảm bảo số lượng EC2 tự động điều chỉnh theo tải, trong khi CloudWatch Alarm giám sát CPU, bộ nhớ, và lưu lượng mạng để gửi thông báo khi vượt ngưỡng.


#### *Lợi ích và hoàn vốn đầu tư (ROI)*  
Lợi ích kỹ thuật:
- Đảm bảo 99.9% uptime nhờ thiết kế đa Availability Zone.
- Giảm độ trễ và tăng tốc độ phản hồi nhờ ALB và routing tối ưu.
- Tăng tính bảo mật bằng cách cách ly lớp backend trong private subnet.
- Tự động mở rộng tài nguyên khi lưu lượng tăng, giảm chi phí khi tải giảm.
- Giám sát hệ thống tập trung và cảnh báo chủ động.

Hiệu quả đầu tư (ROI):
- Tiết kiệm chi phí vận hành 20–40% so với hạ tầng cố định.
- Giảm rủi ro downtime → tăng trải nghiệm người dùng → tăng doanh thu.
- Hạ tầng có thể tái sử dụng, mở rộng dễ dàng cho các dự án khác.

### 3. Kiến trúc giải pháp  
#### *Dịch vụ AWS sử dụng*
- *Route 53*: Quản lý DNS, định tuyến domain, hỗ trợ health check.
- *ACM (AWS Certificate Manager)*: Cấp phát và tự động gia hạn chứng chỉ SSL/TLS cho HTTPS.
- *VPC (Virtual Private Cloud)*: Tạo môi trường mạng riêng biệt cho toàn bộ hệ thống.
- *NAT Gateway*: Cho phép EC2 trong private subnet truy cập internet để update mà không cần public IP.
- *IGW*: Kết nối mạng VPC với Internet.
- *EC2 Instances (App, API, WebSocket)*: Máy chủ xử lý ứng dụng, chạy trong private subnet.    
- *Auto scaling group*: Tự động điều chỉnh số lượng EC2 theo tải.
- *Application Load Balancer (ALB)*: Phân phối lưu lượng giữa các EC2 Web/API/WebSocket.
- *Amazon CloudWatch*: Giám sát hiệu năng, thu thập log và gửi cảnh báo khi có sự cố.
- *Amazon SNS*: Gửi cảnh báo qua email/SMS khi có sự cố.
- *S3 (Simple Store Service)*: Lưu trữ log truy cập từ ALB.

#### *Thiết kế thành phần*  
Hệ thống backend gồm ba lớp chính:
1. Lớp Mạng (Network Layer): Lớp mạng chịu trách nhiệm kết nối, bảo mật và định tuyến lưu lượng giữa người dùng Internet và các tài nguyên nội bộ trong VPC.

   - Các thành phần chính gồm:

        - *Amazon Route 53*: Cung cấp DNS toàn cầu, chịu trách nhiệm phân giải tên miền của ứng dụng đến địa chỉ IP của Application Load Balancer (ALB) đặt tại vùng us-east-1. Route 53 đảm bảo khả năng truy cập nhanh, ổn định và hỗ trợ cân bằng tải giữa các vùng nếu mở rộng đa vùng trong tương lai.

        - *Internet Gateway (IGW)*:Cho phép lưu lượng Internet vào và ra khỏi VPC, đóng vai trò là cổng kết nối chính giữa AWS Cloud và người dùng cuối.

        - *Application Load Balancer (ALB)*:Là điểm truy cập duy nhất cho toàn bộ lưu lượng bên ngoài. ALB phân phối lưu lượng đến các nhóm EC2 backend (Web, API, WebSocket) dựa trên loại request hoặc đường dẫn. Hỗ trợ ACM (AWS Certificate Manager) để mã hóa HTTPS, đảm bảo an toàn dữ liệu khi truyền qua Internet.

        - *NAT Gateway*: Nằm trong Public Subnet, cho phép các EC2 trong Private Subnet truy cập Internet (ví dụ: tải gói cập nhật, truy xuất API bên ngoài) mà không bị lộ IP công khai, tăng cường bảo mật hệ thống.

2. Lớp Ứng Dụng (Application Layer): Lớp này tập trung xử lý logic nghiệp vụ và cung cấp dịch vụ cho người dùng thông qua các EC2 instance.

   - Các thành phần bao gồm:

        - *EC2 Instances (Web, API, WebSocket)*: Các EC2 nằm trong Private Subnet, không thể truy cập trực tiếp từ Internet. Mỗi nhóm EC2 có Security Group riêng biệt, chỉ cho phép lưu lượng từ ALB hoặc NAT Gateway.

        - *Auto Scaling Group (ASG)*: Tự động mở rộng hoặc thu hẹp số lượng EC2 instance dựa trên tải thực tế (ví dụ: CPU > 70%). Giúp đảm bảo hiệu năng, giảm chi phí và tăng độ tin cậy cho ứng dụng.

3. Lớp Giám Sát & Quản Lý (Monitoring & Management Layer): Lớp này đảm nhiệm việc thu thập log, giám sát hiệu năng, cảnh báo sự cố và lưu trữ dữ liệu phục vụ kiểm tra hoặc tối ưu hóa.

   - Các thành phần bao gồm:

        - *Amazon S3*: Nhận và lưu trữ log truy cập từ ALB.

        - *Amazon CloudWatch*: Thu thập các metric như CPU từ EC2. Tạo alarm khi CPU > 80% hoặc khi có dấu hiệu hệ thống quá tải. Cung cấp dashboard trực quan giúp đội ngũ kỹ thuật theo dõi hiệu năng thời gian thực.

        - *Amazon SNS*: Nhận cảnh báo từ CloudWatch và gửi thông báo tự động qua email/SMS đến đội ngũ vận hành khi có sự cố.

#### Tổng quan luồng hoạt động chính
1. Người dùng truy cập tên miền được định tuyến qua Route 53 → chuyển hướng đến ALB qua HTTPS (được bảo mật bằng ACM).
2. ALB kiểm tra loại yêu cầu và định tuyến đến nhóm EC2 backend phù hợp trong Private Subnet.
3. Các EC2 backend xử lý yêu cầu và trả kết quả về cho ALB → ALB trả lại phản hồi cho người dùng.
4. Trong quá trình hoạt động:
    - ALB gửi log truy cập về S3.
    - CloudWatch giám sát hiệu năng, tạo alarm nếu vượt ngưỡng.
    - SNS gửi thông báo đến đội ngũ kỹ thuật khi có sự cố.
    - Auto Scaling tự động tăng/giảm số lượng EC2 khi cần thiết.
5. Các EC2 trong Private Subnet sử dụng NAT Gateway để truy cập Internet khi cần cập nhật hệ thống (khi cần tải bản cập nhật).

### 4. Triển khai kỹ thuật  
#### *Các giai đoạn triển khai*  
1. *Nghiên cứu và vẽ kiến trúc*: Nghiên cứu và thiết kế kiến trúc AWS.  
2. *Tính toán chi phí và kiểm tra tính khả thi*: Sử dụng AWS Pricing Calculator để ước tính và điều chỉnh.  
3. *Điều chỉnh kiến trúc để tối ưu chi phí/giải pháp*: Tinh chỉnh để đảm bảo hiệu quả.  
4. *Phát triển, kiểm thử, triển khai*: Triển khai hệ thống.  

#### *Yêu cầu kỹ thuật*  
1. VPC: 1 VPC với 2 AZ (Multi-AZ).
2. Subnet: 2 Public Subnet, 2 Private Subnet.
3. Instances: Tối thiểu 3 EC2 (Web, API, WebSocket).
4. Auto Scaling: Kích hoạt khi CPU > 70%.
5. Monitoring: CloudWatch + SNS alert.
6. Logging: ALB Access Logs → S3 bucket.
7. Traffic Encryption: HTTPS (ACM certificate).

### 5. Lộ trình & Mốc triển khai  
- Thực tập (tháng 1-3): 3 tháng.
    - Tháng 1: Tìm hiểu, học sử dụng các dịch vụ AWS.
    - Tháng 2: Tìm hiểu, thiết kế, tính giá, điều chỉnh kiến trúc. 
    - Tháng 3: Thực hiện, kiểm thử, ra mắt. 

### 6. Ước tính ngân sách  
Có thể xem chi phí trên [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=5177a11066447369fbffcd58f36842343e069f71) .

#### *Chi phí hạ tầng*  
- Route 53: 2,25 USD/tháng (1 hosted zones, basic check within and outside AWS).  
- S3 Standard: 0,17 USD/tháng (5 GB, PUT, COPY, POST, LIST 10000 request).  
- ACM: 0 USD/tháng
- VPC: 32,89 USD/tháng (22 days working, 1 NAT gateway)
- EC2: 18,18 USD/tháng (Workloads monthly (Baseline: 2, Peak: 5), instnace: t3-micro, pricing: on-demand  )
- SNS: 0 USD/tháng (1 mil/request/month)
- Cloudwatch: 1,80 USD/tháng (Alarm CPU, Request count per target)

*Tổng*: 55,29 USD/tháng

### 7. Đánh giá rủi ro  
#### *Ma trận rủi ro*  
| Loại rủi ro            | Mức độ     | Ảnh hưởng  | Mô tả                                 |
| ---------------------- | ---------- | ---------- | ------------------------------------- |
| Sự cố EC2              | Cao        | Trung bình | Instance lỗi hoặc mất kết nối         |
| Lỗi NAT Gateway        | Trung bình | Cao        | Private subnet mất truy cập Internet  |
| ALB quá tải            | Trung bình | Cao        | Ứng dụng không phản hồi               |
| Sai cấu hình bảo mật   | Cao        | Cao        | Lộ dữ liệu hoặc tấn công từ bên ngoài |
| Chi phí vượt ngân sách | Trung bình | Trung bình | Auto Scaling mở rộng quá mức          |
 

#### *Chiến lược giảm thiểu*  
- Multi-AZ Deployment: EC2 phân tán qua 2 AZ để giảm downtime.
- Auto Scaling Policy: Giới hạn số lượng EC2 tối đa.
- CloudWatch Alarm: Giám sát tải và cảnh báo tức thì.
- Security Review: Định kỳ kiểm tra Security Group, IAM, và log.

#### *Kế hoạch dự phòng*  
- Chi phí vượt ngưỡng → Kích hoạt AWS Budgets alarm, scale down non-prod resources
- Log đầy → Chuyển log sang Glacier hoặc xóa log cũ tự động.  

### 8. Kết quả kỳ vọng  
#### Cải thiện kỹ thuật
- Giảm downtime nhờ HA, multi-AZ, ALB health check.
- Chi phí tối ưu hơn nhờ auto scaling
- Tự động hóa giám sát và cảnh báo giúp phản ứng nhanh hơn khi có sự cố.

#### Giá trị dài hạn
- Dễ tích hợp thêm CI/CD, hệ thống giám sát nâng cao, và Data Pipeline.
- Kiến trúc có thể mở rộng thành mô hình serverless hoặc container-based trong tương lai.