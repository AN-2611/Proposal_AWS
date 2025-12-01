---
title: "Đề Xuất"
date: "2025-09-08"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# AWS APPLICATION LOAD BALANCER
## TRIỂN KHAI CÁC TÍNH NĂNG NÂNG CAO CỦA AWS APPLICATION LOAD BALANCER

![ALB](/images/arc.jpeg)

### 1. Tóm Tắt Điều Hành
Báo cáo này trình bày đánh giá và đề xuất triển khai kiến trúc hệ thống web có tính sẵn sàng cao và bảo mật trên nền tảng AWS, được triển khai tại khu vực us-east-1.  
Kiến trúc bao gồm các thành phần: Route 53, Certificate Manager (ACM), Application Load Balancer (ALB), Auto Scaling Group, CloudWatch, S3, và các phiên bản EC2 chạy trong private subnets trên hai Availability Zones.

Mục tiêu của kiến trúc này là xây dựng một hệ thống ổn định, có khả năng mở rộng, tiết kiệm chi phí và an toàn, hỗ trợ dịch vụ Web, API, và WebSocket trong môi trường sản xuất.

### 2. Vấn Đề
#### *Các Vấn Đề Hiện Tại*
Trong nhiều hệ thống web truyền thống hoặc hạ tầng on-premises, thường xảy ra các vấn đề sau:

- Chi phí đầu tư và bảo trì cao: Phần cứng, thiết bị lưu trữ, hệ thống mạng và nhân sự kỹ thuật yêu cầu chi phí ban đầu lớn. Ngoài ra, việc bảo trì, nâng cấp và thay thế định kỳ làm tăng tổng chi phí sở hữu (TCO).

- Khả năng mở rộng thủ công: Khi lưu lượng tăng đột ngột, việc mở rộng hạ tầng phải thực hiện thủ công, tốn thời gian và có thể gián đoạn dịch vụ. Nhiều hệ thống phải cấp phát dư thừa tài nguyên để đảm bảo an toàn, dẫn đến lãng phí.

- Khả năng chịu lỗi thấp: Một lỗi phần cứng, lỗi cấu hình hoặc mất điện có thể làm gián đoạn toàn bộ backend. Việc triển khai cơ chế dự phòng và tự phục hồi khó khăn trong hạ tầng vật lý truyền thống.

- Giám sát và xử lý sự cố hạn chế: Hệ thống on-premises thường thiếu công cụ quan sát tập trung. Việc phát hiện sự cố, theo dõi hiệu năng hoặc phân tích log phải thực hiện thủ công, làm chậm quá trình xử lý.

- Khối lượng công việc bảo mật và tuân thủ lớn: Việc duy trì tường lửa, quản lý bản vá, kiểm soát truy cập và sao lưu dữ liệu phải thực hiện thủ công, dễ xảy ra lỗi và tốn nhiều nguồn lực.

Những hạn chế này dẫn đến chu kỳ phát triển phần mềm chậm hơn, chi phí vận hành cao hơn, độ tin cậy thấp hơn và thiếu linh hoạt để đáp ứng sự thay đổi nhanh chóng của ứng dụng web hiện đại.

#### *Giải Pháp*
Giải pháp đề xuất là triển khai ứng dụng web theo kiến trúc **3 tầng** trên AWS, bao gồm:
- **Tầng Trình Bày:** Người dùng truy cập hệ thống thông qua Route 53 và ALB qua HTTPS (được bảo mật bằng chứng chỉ ACM).
- **Tầng Ứng Dụng:** Chạy trên các phiên bản EC2 trong private subnets, chia thành ba nhóm dịch vụ: Web, API, và WebSocket.
- **Tầng Dữ Liệu & Giám Sát:** Lưu trữ log trong S3, giám sát tài nguyên qua CloudWatch, và gửi cảnh báo qua SNS.

Auto Scaling Groups tự động điều chỉnh số lượng EC2 dựa trên tải, trong khi CloudWatch Alarms giám sát CPU, bộ nhớ và mạng để gửi cảnh báo khi vượt ngưỡng.

#### *Lợi Ích và Hiệu Quả Đầu Tư (ROI)*
**Lợi ích kỹ thuật:**
- Đảm bảo uptime 99.9% nhờ thiết kế multi-AZ.  
- Giảm độ trễ và cải thiện thời gian phản hồi nhờ ALB và định tuyến tối ưu.  
- Tăng cường bảo mật bằng cách cô lập backend trong private subnets.  
- Tự động mở rộng tài nguyên theo tải, giảm chi phí nhàn rỗi.  
- Giám sát tập trung và cảnh báo chủ động.

**Hiệu quả đầu tư (ROI):**
- Giảm chi phí vận hành 20–40% so với hạ tầng cố định.  
- Giảm downtime → cải thiện trải nghiệm người dùng → tăng doanh thu.  
- Hạ tầng có thể tái sử dụng và dễ mở rộng cho các dự án tương lai.

### 3. Kiến Trúc Giải Pháp
#### *Các Dịch Vụ AWS Sử Dụng*
- *Route 53*: Quản lý DNS, định tuyến lưu lượng tên miền, hỗ trợ health checks.  
- *ACM (AWS Certificate Manager)*: Cấp và tự động gia hạn chứng chỉ SSL/TLS cho HTTPS.  
- *VPC (Virtual Private Cloud)*: Cung cấp môi trường mạng riêng biệt cho hệ thống.  
- *NAT Gateway*: Cho phép EC2 trong private subnets truy cập Internet để cập nhật mà không cần IP công khai.  
- *IGW*: Kết nối VPC với Internet.  
- *EC2 Instances (App, API, WebSocket)*: Máy chủ backend chạy trong private subnets.  
- *Auto Scaling Group*: Tự động điều chỉnh số lượng EC2 theo tải.  
- *Application Load Balancer (ALB)*: Phân phối lưu lượng giữa các EC2 cho Web/API/WebSocket.  
- *Amazon CloudWatch*: Giám sát hiệu năng, thu thập log, kích hoạt cảnh báo khi có sự cố.  
- *Amazon SNS*: Gửi thông báo cảnh báo qua email/SMS.  
- *S3 (Simple Storage Service)*: Lưu trữ log truy cập ALB.

#### *Thiết Kế Thành Phần*
Hệ thống backend gồm ba lớp chính:

1. **Tầng Mạng:** Đảm bảo kết nối, bảo mật và định tuyến giữa người dùng Internet và tài nguyên nội bộ VPC.  
   - Thành phần chính:
     - *Amazon Route 53*: DNS toàn cầu, phân giải tên miền ứng dụng đến IP ALB tại us-east-1.  
     - *Internet Gateway (IGW)*: Cho phép lưu lượng Internet vào/ra VPC.  
     - *Application Load Balancer (ALB)*: Điểm vào duy nhất cho lưu lượng bên ngoài, phân phối yêu cầu đến các nhóm EC2 backend (Web, API, WebSocket). Tích hợp với *AWS Certificate Manager (ACM)* để mã hóa HTTPS.  
     - *NAT Gateway*: Nằm trong Public Subnet, cho phép EC2 trong Private Subnets truy cập Internet mà không cần IP công khai.  

2. **Tầng Ứng Dụng:** Xử lý logic nghiệp vụ và cung cấp dịch vụ qua các phiên bản EC2.  
   - Thành phần:
     - *EC2 Instances (Web, API, WebSocket)*: Nằm trong Private Subnets, không thể truy cập trực tiếp từ Internet.  
     - *Auto Scaling Group (ASG)*: Tự động tăng/giảm số lượng EC2 theo tải thực tế (ví dụ CPU > 70%).  

3. **Tầng Giám Sát & Quản Lý:** Thu thập log, giám sát hiệu năng, cảnh báo và lưu trữ dữ liệu.  
   - Thành phần:
     - *Amazon S3*: Lưu trữ log truy cập ALB.  
     - *Amazon CloudWatch*: Thu thập chỉ số, kích hoạt cảnh báo khi CPU > 80% hoặc có dấu hiệu quá tải.  
     - *Amazon SNS*: Nhận cảnh báo từ CloudWatch và gửi thông báo cho đội vận hành.  

#### *Luồng Hoạt Động Chính*
1. Người dùng truy cập tên miền qua Route 53 → chuyển đến ALB qua HTTPS (ACM).  
2. ALB kiểm tra loại yêu cầu và định tuyến đến nhóm EC2 backend phù hợp.  
3. EC2 xử lý yêu cầu và trả kết quả cho ALB → ALB phản hồi người dùng.  
4. Trong quá trình hoạt động:  
   - ALB gửi log truy cập đến S3.  
   - CloudWatch giám sát hiệu năng và kích hoạt cảnh báo.  
   - SNS gửi thông báo cho đội vận hành.  
   - Auto Scaling tự động tăng/giảm EC2 khi cần.  
5. EC2 trong Private Subnets dùng NAT Gateway để truy cập Internet (ví dụ tải bản cập nhật).  

### 4. Triển Khai Kỹ Thuật
#### *Các Giai Đoạn Triển Khai*
1. *Nghiên cứu và thiết kế kiến trúc:* Tìm hiểu và thiết kế kiến trúc AWS.  
2. *Ước tính chi phí và kiểm tra khả thi:* Sử dụng AWS Pricing Calculator để ước tính chi phí.  
3. *Tối ưu kiến trúc:* Điều chỉnh để tối ưu chi phí và hiệu năng.  
4. *Phát triển, kiểm thử, triển khai:* Thực hiện và kiểm thử hệ thống.  

#### *Yêu Cầu Kỹ Thuật*
1. VPC: 1 VPC với 2 AZs (Multi-AZ).  
2. Subnets: 