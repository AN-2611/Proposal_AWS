---
title: "Bản đề xuất"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 2. </b> "
---


# AWS APPLICATION LOAD BALANCER
## TRIỂN KHAI CÁC TÍNH NĂNG NÂNG CAO CỦA AWS APPLICATION LOAD BALANCER 

![ALB](/images/arc.jpeg)

### 1. Tóm tắt điều hành  
Báo cáo này trình bày đánh giá và đề xuất xây dựng, triển khai và quản lý một ứng dụng web ba tầng (three-tier web application) được đóng gói (containerized) có khả năng mở rộng cao (highly scalable) cho các doanh nghiệp vừa và nhỏ.

Mục tiêu của kiến trúc là cung cấp một khuôn khổ hoàn chỉnh, từ thiết kế đến vận hành, để xây dựng một ứng dụng web bền vững, hiệu quả về chi phí và có khả năng mở rộng cao thông qua việc tận dụng công nghệ container trên AWS.

### 2. Tuyên bố vấn đề
#### *Vấn đề hiện tại*  
Các ứng dụng web bán hàng truyền thống thường tồn tại các vấn đề sau:

- Chi phí đầu tư và bảo trì cao: Việc đầu tư phần cứng, thiết bị lưu trữ, hệ thống mạng và nguồn nhân lực kỹ thuật yêu cầu chi phí ban đầu lớn. Ngoài ra, chi phí bảo trì, nâng cấp và thay thế định kỳ khiến tổng chi phí sở hữu (TCO) tăng cao.

- Thiếu khả năng mở rộng tự dộng: Khi lưu lượng truy cập tăng đột biến, việc mở rộng hạ tầng phải thực hiện thủ công, mất nhiều thời gian và có thể gây gián đoạn dịch vụ trong giờ cao điểm (ví dụ: flash sale, ngày lễ,...). Nhiều hệ thống phải đầu tư dư thừa tài nguyên để phòng ngừa, dẫn đến lãng phí công suất. 

- Khả năng chịu lỗi thấp: Một sự cố phần cứng, lỗi cấu hình hoặc mất điện có thể làm gián đoạn toàn bộ hệ thống.

- Khó giám sát và khắc phục sự cố: Hệ thống on-premises thường thiếu công cụ quan sát và giám sát tập trung. Việc phát hiện sự cố, theo dõi hiệu năng hoặc phân tích log đòi hỏi thao tác thủ công, làm chậm quá trình phản ứng và khắc phục.

- Gánh nặng bảo mật và tuân thủ: Việc duy trì tường lửa, quản lý bản vá bảo mật, kiểm soát truy cập và sao lưu dữ liệu phải thực hiện thủ công, dễ sai sót và tiêu tốn nguồn lực vận hành.

- Thiếu khả năng tương tác tự động và tức thời với khách hàng: Đội ngũ hỗ trợ phải xử lý lặp lại các câu hỏi cơ bản về sản phẩm và tồn kho. Khách hàng rời đi vì không nhận được câu trả lời nhanh chóng về chi tiết sản phẩm

Những hạn chế này khiến chu trình phát triển phần mềm chậm, chi phí vận hành cao, độ tin cậy thấp, và thiếu tính linh hoạt cần thiết để đáp ứng nhu cầu thay đổi nhanh của các ứng dụng web hiện đại.

#### *Giải pháp*  

Giải pháp đề xuất là chuyển sang kiến trúc serverless và containerized trên AWS, trong đó:
- Amazon ECS với Fargate chạy backend trong private subnet.
- Amazon API Gateway + PrivateLink làm cầu nối an toàn giữa lớp API và backend.
- Amazon Lambda + Bedrock dùng để xây dựng Chat Widget AI trả lời câu hỏi người dùng.
- Amazon DynamoDB lưu trữ dữ liệu sản phẩm, tồn kho, giá.
- Amazon ElastiCache hỗ trợ cache dữ liệu giúp giảm độ trễ.
- Toàn bộ hoạt động được giám sát qua CloudWatch và quản lý truy cập qua Cognito.

#### *Lợi ích và hoàn vốn đầu tư (ROI)*  
Lợi ích kỹ thuật:
- Đảm bảo 99.9% uptime nhờ thiết kế đa Availability Zone.
- Giảm độ trễ và tăng tốc độ phản hồi nhờ ALB và routing tối ưu.
- Tăng tính bảo mật bằng cách cách ly lớp backend trong private subnet.
- Tự động mở rộng tài nguyên khi lưu lượng tăng, giảm chi phí khi tải giảm.
- Giám sát hệ thống và cảnh báo chủ động.

Hiệu quả đầu tư (ROI):
- Tiết kiệm chi phí vận hành.
- Giảm rủi ro downtime → tăng trải nghiệm người dùng → tăng doanh thu.
- Hạ tầng có thể tái sử dụng, mở rộng dễ dàng cho các dự án khác.

### 3. Kiến trúc giải pháp  
#### *Dịch vụ AWS sử dụng*
- *Route 53*: Quản lý DNS, định tuyến domain, hỗ trợ health check.
- Amazon CloudFront: Phân phối nội dung tĩnh qua CDN, tối ưu tốc độ truy cập toàn cầu.
- Amazon S3: Lưu trữ và phục vụ các tệp tĩnh như HTML, CSS, JS, hình ảnh.
- Amazon Cognito: Quản lý xác thực người dùng, hỗ trợ đăng nhập/đăng ký an toàn.
- AWS WAF (Web Application Firewall): Bảo vệ ứng dụng khỏi các cuộc tấn công phổ biến như SQL Injection, XSS, hoặc bot traffic.
- Amazon API Gateway: Cung cấp endpoint an toàn cho các dịch vụ backend. Kết nối riêng tư với ALB thông qua PrivateLink (VPC Endpoint) nhằm đảm bảo dữ liệu không ra Internet công cộng.
- Application Load Balancer (ALB): Cân bằng tải giữa các container ECS/Fargate trong private subnet, hỗ trợ routing dựa trên đường dẫn và header.
- Amazon ECS (Elastic Container Service) với Fargate: Chạy các container backend không cần quản lý máy chủ, đảm bảo khả năng mở rộng linh hoạt.
- Amazon ECR: Lưu trữ container image.
- Amazon Lambda: Xử lý các yêu cầu serverless như logic tra cứu dữ liệu, gọi API nội bộ hoặc truy cập Amazon Bedrock cho Chat Widget.
- Amazon DynamoDB: Lưu trữ thông tin sản phẩm, tồn kho, giá, và metadata về phản hồi chatbot với khả năng mở rộng cao và truy xuất nhanh.
- Amazon ElastiCache (Redis): Lưu trữ tạm (cache) dữ liệu đã scrape từ các trang sản phẩm giúp giảm thời gian phản hồi và hạn chế việc truy cập lại nguồn.
- Amazon Bedrock: Cung cấp mô hình ngôn ngữ Generative AI cho Chat Widget, hỗ trợ người dùng truy vấn thông tin sản phẩm tự nhiên.
- Amazon CloudWatch: Giám sát hiệu năng, log ECS, log ALB và thiết lập cảnh báo cho các lỗi bất thường.

#### *Thiết kế thành phần*  
Hệ thống backend gồm ba lớp chính:

1️⃣ Tầng Presentation (Frontend Layer)

Mục tiêu: Cung cấp giao diện web và điểm truy cập duy nhất cho người dùng cuối.
Dịch vụ sử dụng:
- Amazon Route 53: Quản lý tên miền và DNS, định tuyến truy cập tới ứng dụng.
- Amazon CloudFront: Phân phối nội dung (CDN) giúp giảm độ trễ và tăng hiệu năng truy cập toàn cầu.
- Amazon S3: Lưu trữ nội dung tĩnh (HTML, CSS, JS, hình ảnh).
- Amazon Cognito: Quản lý đăng nhập, xác thực và quyền truy cập người dùng.

2️⃣ Tầng Application (Logic Layer)

Mục tiêu: Xử lý logic nghiệp vụ, API, chatbot và điều phối yêu cầu từ người dùng.
Dịch vụ sử dụng:
- Amazon API Gateway: Là điểm đầu vào cho tất cả các request API từ frontend.
- AWS PrivateLink (VPC Link): Cho phép kết nối riêng tư giữa API Gateway và Application Load Balancer mà không đi qua Internet.
- Application Load Balancer (ALB): Phân phối lưu lượng đến các container backend.
Amazon ECS (với AWS Fargate): Triển khai và vận hành các container backend trong môi trường serverless, tự động mở rộng khi tải tăng.
- AWS Lambda: Xử lý các tác vụ logic nhỏ, chatbot, tương tác với Amazon Bedrock.
- Amazon Bedrock: Nền tảng AI Generative (LLM) được dùng để xây dựng Chat Widget thông minh, giúp người dùng đặt câu hỏi về sản phẩm, giá, hoặc thành phần.

3️⃣ Tầng Data (Database Layer)

Mục tiêu: Lưu trữ, truy xuất và cache dữ liệu sản phẩm, giá, tồn kho và thông tin hỗ trợ chatbot.
Dịch vụ sử dụng:

- Amazon DynamoDB: Lưu trữ dữ liệu sản phẩm, giá và thông tin tồn kho theo mô hình NoSQL hiệu năng cao.
- Amazon ElastiCache (Redis): Cache dữ liệu truy vấn thường xuyên, giảm độ trễ truy cập.
- Amazon CloudWatch: Giám sát toàn bộ hoạt động, thu thập log, metric và cảnh báo.
- Amazon ECR: Lưu trữ container image phục vụ cho ECS deployment.
#### Tổng quan luồng hoạt động chính
1. Người dùng truy cập ứng dụng web thông qua Amazon Route 53, được định tuyến đến Amazon CloudFront – dịch vụ CDN phân phối nội dung tĩnh (HTML, CSS, JS) được lưu trữ trên Amazon S3.
2. Khi người dùng thực hiện hành động, ví dụ như xem thông tin sản phẩm “A”, yêu cầu sẽ được gửi từ frontend đến Amazon API Gateway.
3. API Gateway chuyển tiếp yêu cầu thông qua VPC Endpoint (AWS PrivateLink) đến Application Load Balancer (ALB) trong private subnet, đảm bảo toàn bộ kết nối nội bộ an toàn và không đi qua Internet công cộng.
4. ALB phân phối yêu cầu đến các container ứng dụng chạy trên Amazon ECS (Fargate) để xử lý nghiệp vụ, như truy vấn dữ liệu sản phẩm, tồn kho, hoặc giá bán từ Amazon DynamoDB.
5. Khi người dùng sử dụng Chat Widget để đặt câu hỏi về sản phẩm, yêu cầu sẽ được gửi đến AWS Lambda, sau đó gọi Amazon Bedrock để xử lý ngôn ngữ tự nhiên và hiểu ý định của người dùng.
6. Lambda hoặc ECS sẽ kiểm tra dữ liệu sản phẩm trong Amazon DynamoDB.
    - Nếu DynamoDB chưa có thông tin chi tiết (ví dụ: mô tả, công dụng, thành phần), hệ thống sẽ gọi Amazon Bedrock để tổng hợp nội dung hoặc thực hiện scraping dữ liệu web.
    - Thông tin thu được sẽ được lưu lại vào Amazon ElastiCache nhằm tái sử dụng cho các truy vấn sau, giúp giảm độ trễ và tải hệ thống.
1. Kết quả cuối cùng được trả về API Gateway, sau đó phản hồi đến frontend (ứng dụng web) để hiển thị cho người dùng.
2. Trong suốt quá trình xử lý, log và metric từ các thành phần (ALB, ECS, DynamoDB) được gửi về Amazon CloudWatch để giám sát hiệu năng, phát hiện lỗi và hỗ trợ phân tích vận hành hệ thống.

### 4. Triển khai kỹ thuật  
#### *Các giai đoạn triển khai*  
1. *Nghiên cứu và vẽ kiến trúc*: Nghiên cứu và thiết kế kiến trúc AWS.  
2. *Tính toán chi phí và kiểm tra tính khả thi*: Sử dụng AWS Pricing Calculator để ước tính và điều chỉnh.  
3. *Điều chỉnh kiến trúc để tối ưu chi phí/giải pháp*: Tinh chỉnh để đảm bảo hiệu quả.  
4. *Phát triển, kiểm thử, triển khai*: Triển khai hệ thống.  

#### *Yêu cầu kỹ thuật*  
1. VPC: 1 VPC với 2 AZ (Multi-AZ).
2. ECS Service chạy trên Fargate (tối thiểu 2 AZ).
3. Cognito xác thực, quản lý người dùng. 
4. S3 bucket chứa web, có CloudFront Distribution.
5. WAF bảo vệ trang web
6. API Gateway có VPC Link đến ALB.
7. Private subnet có VPC Endpoint để pull Docker Image từ ECR
8. Monitoring: CloudWatch.


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
| **Rủi ro**                                  | **Mức độ** | **Ảnh hưởng** | **Loại**  | **Mô tả**                                                                                                                          |
| ------------------------------------------- | ---------- | ------------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| Lỗi cấu hình **PrivateLink**                | Cao        | Trung bình    | Kỹ thuật  | Gây gián đoạn kết nối giữa API Gateway và ALB, khiến các dịch vụ backend không thể truy cập nội bộ.                                |
| Tăng **chi phí sử dụng Fargate và Bedrock API**        | Trung bình | Cao           | Tài chính | Khi người dùng truy vấn hoặc dùng Chat Widget quá nhiều hoặc mô hình AI được gọi với tần suất cao, chi phí inference có thể tăng nhanh.      |
| **Quá tải ECS/Fargate service**             | Cao        | Cao           | Hiệu năng | Khi lưu lượng tăng đột biến, ECS có thể quá tải nếu autoscaling không được cấu hình phù hợp, ảnh hưởng đến thời gian phản hồi API. |
| **Cấu hình CloudFront/WAF không chính xác** | Thấp       | Trung bình    | Bảo mật   | Nếu thiết lập rule WAF hoặc cache policy sai, có thể dẫn đến lỗi truy cập hoặc rủi ro bảo mật từ traffic bên ngoài.                |

 

#### *Chiến lược giảm thiểu*  
- Multi-AZ Deployment: Dự phòng Fargate service ở AZ thứ hai.
- Thiết lập cảnh báo qua Amazon CloudWatch cho cả chi phí vận hành (Cost Alarms) và hiệu năng (Performance Metrics) nhằm phát hiện sớm bất thường.


#### *Kế hoạch dự phòng*  
- Chi phí vượt ngưỡng → Kích hoạt AWS Budgets alarm, scale down non-prod resources

### 8. Kết quả kỳ vọng  
#### Cải thiện kỹ thuật
- Giảm downtime nhờ HA, multi-AZ, ALB health check.
- Chi phí tối ưu hơn, Tích hợp AI Chat hỗ trợ người dùng
- Tự động hóa giám sát và cảnh báo giúp phản ứng nhanh hơn khi có sự cố.

#### Giá trị dài hạn
- Mở rộng linh hoạt để thêm module thương mại điện tử, analytics hoặc recommendation engine.
- Dễ tích hợp thêm CI/CD, hệ thống giám sát nâng cao, và Data Pipeline.
