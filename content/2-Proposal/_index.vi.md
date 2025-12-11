---
title: "Bản Đề Xuất"
date: "2025-09-08"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

## 1. TÓM TẮT ĐIỀU HÀNH

### 1.1 Tổng quan dự án

NutriChat là ứng dụng web trợ lý dinh dưỡng thông minh, hỗ trợ người dùng xây dựng chế độ ăn uống lành mạnh dựa trên nhu cầu cá nhân. Ứng dụng sử dụng mô hình AI Claude 3 Haiku thông qua dịch vụ AWS Bedrock để phân tích dữ liệu dinh dưỡng, tạo ra gợi ý phù hợp với thể trạng, mục tiêu sức khỏe và thói quen ăn uống của từng người.

Hệ thống được triển khai hoàn toàn trên nền tảng AWS với kiến trúc hiện đại theo hướng serverless, giúp tối ưu chi phí, tăng khả năng mở rộng và giảm tải vận hành. Kiến trúc đảm bảo các nguyên tắc của AWS Well-Architected Framework gồm: bảo mật, hiệu năng, độ tin cậy, tối ưu chi phí, và vận hành.

### 1.2 Mục tiêu chính

- Xây dựng hệ thống tư vấn dinh dưỡng tự động.
- Cá nhân hóa lời khuyên dựa trên profile, dị ứng, mục tiêu sức khỏe
- Triển khai trên AWS với khả năng sẵn sàng cao và tự động mở rộng
- Đảm bảo bảo mật dữ liệu người dùng.
- Tối ưu chi phí vận hành.

### 1.3 Kết quả đạt được

**Thành công 100%** - Dự án đã được triển khai hoàn chỉnh cơ bản với tất cả tính năng hoạt động ổn định:

- **Hạ tầng**: AWS resources được quản lý bằng Terraform
- **Xác thực**: AWS Cognito với JWT, xác minh email
- **Tích hợp AI**: Claude 3 Haiku với phản hồi streaming
- **Cơ sở dữ liệu**: PostgreSQL Multi-AZ với sao lưu tự động
- **Giao diện**: Vue.js responsive UI trên CloudFront CDN
- **Giám sát**: CloudWatch với nhật ký, số liệu, cảnh báo

**URL Production**: https://d13s9jdjslcf4.cloudfront.net



---

## 2. PHÁT BIỂU VẤN ĐỀ

### 2.1 Vấn đề là gì?

#### Vấn đề hiện tại trong lĩnh vực tư vấn dinh dưỡng

**1. Chi phí tư vấn cao**
- Tư vấn dinh dưỡng 1-1 với chuyên gia
- Không phải ai cũng có khả năng chi trả
- Thời gian chờ đợi lịch hẹn lâu (1-2 tuần)

**2. Thiếu tính cá nhân hóa**
- Thông tin dinh dưỡng trên internet mang tính tổng quát
- Không xem xét dị ứng, sở thích cá nhân
- Không phù hợp với mục tiêu sức khỏe riêng

**3. Khó tiếp cận 24/7**
- Chuyên gia chỉ làm việc giờ hành chính
- Không có hỗ trợ tức thì khi cần
- Khó theo dõi tiến độ liên tục

**4. Rào cản ngôn ngữ và văn hóa**
- Thiếu tư vấn bằng tiếng Việt
- Không phù hợp với văn hóa ẩm thực Việt Nam
- Khó áp dụng lời khuyên từ nước ngoài

### 2.2 Giải pháp

#### Giải pháp NutriChat

**1. Chatbot Được hỗ trợ bởi AI**

- Sử dụng Claude 3 Haiku - mô hình AI tiên tiến
- Phản hồi tức thì, không cần chờ đợi
- Có sẵn 24/7, không giới hạn số lần tư vấn
- Chi phí thấp: ~$0.002/conversation

**2. Công cụ Cá nhân hóa**

- Lưu trữ profile chi tiết: chiều cao, cân nặng, mục tiêu
- Theo dõi dị ứng thực phẩm
- Xem xét chế độ ăn (vegetarian, vegan, keto, v.v.)
- Điều chỉnh lời khuyên theo mức độ hoạt động thể chất

**3. Kiến trúc Hướng tới đám mây**

- Triển khai trên AWS với khả năng sẵn sàng cao
- Tự động mở rộng theo nhu cầu sử dụng
- Triển khai Multi-AZ cho uptime 99.9%
- Mạng phân phối toàn cầu cho tốc độ truy cập nhanh

**4. Bảo mật & Quyền riêng tư**

- AWS Cognito cho xác thực
- JWT tokens với thời gian hết hạn
- Mã hóa khi lưu trữ và khi truyền tải




### 2.3 Lợi ích và Lợi nhuận từ Đầu tư

#### Lợi ích cho người dùng

**1. Tiện lợi**
- Truy cập mọi lúc, mọi nơi
- Phản hồi tức thì (< 3 giây)
- Lưu lịch sử hội thoại để xem lại
- Không cần đi lại, tiết kiệm thời gian.

**2. Cá nhân hóa**
- Lời khuyên phù hợp với profile cá nhân
- Tránh thực phẩm gây dị ứng
- Phù hợp với mục tiêu sức khỏe

**3. Riêng tư**
- Không cần gặp mặt trực tiếp
- Dữ liệu được mã hóa và bảo mật


#### ROI cho nhà đầu tư

- Hiện tại NutriChat đang trong giai đoạn phát triển MVP và chưa triển khai bất kỳ gói trả phí nào cho người dùng. Sản phẩm đang được mở cho cộng đồng sử dụng miễn phí nhằm thu thập ý kiến, đánh giá mức độ hữu ích và hoàn thiện trải nghiệm sản phẩm. Giai đoạn này giúp nhóm phát triển hiểu rõ nhu cầu thực tế, điều chỉnh tính năng và định hình mô hình kinh doanh phù hợp.
- Mặc dù chưa có doanh thu tại thời điểm hiện tại, kết quả khảo sát và phản hồi người dùng cho phép đưa ra dự báo sơ bộ về khả năng thương mại hóa trong tương lai.

**Chi phí vận hành (ước tính)**: $86/tháng (~$1,032/năm) (chi phí có thể thay đổi theo nhu cầu sử dụng thực tế)

**Dự phóng mô hình doanh thu (khi ra mắt chính thức)**:
Nếu sản phẩm đạt 1,000 người dùng tích cực sau khi phát triển đầy đủ, mô hình giá dự kiến có thể bao gồm:
  - Freemium: 70% người dùng (miễn phí để thu hút cộng đồng)
  - Basic Plan: 25% người dùng, dự kiến ~ $5/tháng
  - Premium Plan: 5% người dùng, dự kiến ~ $15/tháng

**Lợi ích kinh doanh dài hạn**
- Tối ưu vận hành: Sử dụng kiến trúc serverless giúp chi phí linh hoạt theo lượng người dùng, tiết kiệm hơn so với hạ tầng cố định truyền thống.
- Khả năng mở rộng: Kiến trúc cloud cho phép mở rộng quy mô và bổ sung gói tính năng nâng cao mà không cần thay đổi hạ tầng.
- Cải thiện trải nghiệm người dùng: Giảm downtime và tăng tốc độ phản hồi với AI → giữ chân người dùng tốt hơn, tăng khả năng chuyển đổi sang gói trả phí.
- Tính tái sử dụng: Nền tảng AI & dữ liệu dinh dưỡng có thể mở rộng sang nhiều sản phẩm mới (meal plan, coaching, nutrition insights).



---

## 3. KIẾN TRÚC GIẢI PHÁP

### 3.1 Các dịch vụ AWS được sử dụng

#### Compute & Container
**Amazon ECS Fargate**
- Nền tảng container Serverless
- Tự động mở rộng 1-4 tasks
- 0.5 vCPU, 1GB RAM mỗi task
- Chi phí: $30-50/tháng

**Application Load Balancer (ALB)**
- Phân phối traffic đến các ECS tasks
- Kiểm tra sức khỏe tự động
- Kết thúc SSL/TLS
- Chi phí: Bao gồm trong ECS

#### Lưu trữ & Cơ sở dữ liệu
**Amazon RDS PostgreSQL**
- Phiên bản db.t3.micro
- Triển khai Multi-AZ
- 20GB lưu trữ với tự động mở rộng
- Sao lưu tự động (giữ lại 7 ngày)
- Chi phí: $15-25/tháng

**Amazon S3**
- Lưu trữ trang web tĩnh
- Kiểm tra phiên bản được bật
- Chính sách vòng đời
- Chi phí: $1/tháng

#### Mạng & Phân phối nội dung
**Amazon CloudFront**
- CDN toàn cầu với 200+ vị trí edge
- Kết thúc HTTPS
- Tối ưu hóa bộ nhớ đệm
- Bảo vệ DDoS
- Chi phí: $0 miễn phí

**Amazon VPC**
- Subnets công cộng (2 AZs)
- Subnets riêng tư (2 AZs)
- Internet Gateway
- NAT Gateway (tùy chọn)
- Security Groups & NACLs
- Chi phí: $3,25/ngày

**VPC Endpoints**
- Bedrock endpoint
- Secrets Manager endpoint
- Kết nối riêng tư
- Chi phí: $7/tháng

#### API & Xác thực
**Amazon API Gateway**
- HTTP API (rẻ hơn REST API)
- JWT Authorizer với Cognito
- Giới hạn tốc độ & điều chỉnh
- Cấu hình CORS
- Chi phí: $3-10/tháng

**Amazon Cognito**
- User Pool cho xác thực
- Xác minh email với OTP
- Chính sách mật khẩu
- Hỗ trợ MFA
- Phát hành token JWT
- Chi phí: Miễn phí (50.000 MAU đầu tiên)

#### AI & Học máy
**Amazon Bedrock**
- Mô hình Claude 3 Haiku
- Phản hồi streaming
- Kết nối VPC endpoint
- Chi phí: $2-10/tháng
  - Đầu vào: $0,00025/1K tokens
  - Đầu ra: $0,00125/1K tokens

#### Bảo mật & Bí mật
**AWS Secrets Manager**
- Thông tin xác thực cơ sở dữ liệu
- Khóa API
- Xoay vòng tự động
- Chi phí: $0,40/20bí mật/tháng

**AWS IAM**
- Vai trò cho các ECS tasks
- Chính sách với đặc quyền tối thiểu
- Xác thực giữa các dịch vụ
- Chi phí: Miễn phí

#### Giám sát & Ghi nhật ký
**Amazon CloudWatch**
- Nhật ký: ECS, ALB, RDS DB
- Số liệu: CPU, Bộ nhớ, Độ trễ
- Cảnh báo: Kích hoạt tự động mở rộng
- Bảng điều khiển: Giám sát thời gian thực
- Chi phí: $5-10/tháng (5GB miễn phí)

**AWS CloudTrail**
- Kiểm tra cuộc gọi API
- Ghi nhật ký tuân thủ
- Chi phí: Miễn phí (sự kiện quản lý)



### 3.2 Component Design

#### Kiến trúc Cấp cao
![image architech](/images/Proposal/Containerized-and-Scalable-Web-Application.drawio.png)

#### Tương tác giữa các thành phần

**1. Luồng Xác thực**
```
User → CloudFront → Cognito: Sign Up/In
Cognito → User: JWT Tokens (Access, ID, Refresh)
User → API Gateway: Request + JWT
API Gateway → Cognito: Verify JWT
API Gateway → ALB → Django: Forward (if valid)
Django → RDS: Query user data
Django → User: Response
```

**2. Luồng Chat**
```
User → API Gateway: POST /api/chat/ + JWT
API Gateway → Django: Forward
Django → RDS: Get user profile
Django → RDS: Save user message
Django → Bedrock: Call Claude 3 + profile context
Bedrock → Django: Stream response (SSE)
Django → User: Stream tokens
Django → RDS: Save AI response
```

**3. Quản lý Profile**
```
User → API Gateway: PUT /api/users/profile/ + JWT
API Gateway → Django: Forward
Django → RDS: Update user profile
Django → User: Success response
```



#### Các Lớp Bảo mật

**Lớp 1: API Gateway**
- Xác minh JWT trước khi request đến backend
- Giới hạn tốc độ: 1000 requests/second
- Điều chỉnh: 500 requests/second per user
- Cấu hình CORS

**Lớp 2: Django Backend**
- Kiểm tra quyền người dùng
- Xác thực đầu vào
- Thực thi quy tắc kinh doanh
- Phòng chống SQL injection (ORM)

**Lớp 3: Mạng VPC**
- Private subnets cho backend
- Không có public IPs cho ECS tasks
- Security Groups: Chỉ cho phép traffic cần thiết
- NACLs: Tường lửa cấp mạng

**Lớp 4: Cơ sở dữ liệu**
- RDS trong private subnet
- Mã hóa khi lưu trữ (AES-256)
- Mã hóa khi truyền tải (TLS)
- Sao lưu tự động
- Xác thực cơ sở dữ liệu IAM

#### Luồng Dữ liệu

**Lưu trữ Dữ liệu Người dùng**
```
AWS Cognito User Pool
    ↓ (cognito_sub)
users_userprofile (RDS)
    ↓ (cognito_sub)
chat_conversation (RDS)
    ↓ (conversation_id)
chat_message (RDS)
```

**Mã hóa Dữ liệu**
- **Khi lưu trữ**: Mã hóa RDS, mã hóa S3
- **Khi truyền tải**: TLS 1.2+ cho tất cả connections
- **Ứng dụng**: Django password hashing (PBKDF2)



---

## 4. TECHNICAL IMPLEMENTATION

### 4.1 Implementation Phases

#### Giai đoạn 1: Nghiên cứu & Lập kế hoạch (Tuần 7)

**Mục tiêu**: Xác định dự án làm về gì, làm rõ mục đích dự án, xác định vấn đề muốn giải quyết.

**Các nhiệm vụ**:
- Xác định dự án làm về gì?
- Xác định đối tượng người dùng, nhu cầu và pain points
- Giải pháp đề xuất, giá trị mang lại
- Thu thập và tổng hợp yêu cầu từ tài liệu và mentor
- Rà soát các use case chính của ứng dụng

---

#### Giai đoạn 2: Nghiên cứu & Lập kế hoạch Kiến trúc (Tuần 8)

**Mục tiêu**: Làm rõ mục đích dự án, xác định vấn đề muốn giải quyết, phạm vi thực hiện, và xây dựng bản thiết kế kiến trúc hệ thống phù hợp.

**Các nhiệm vụ**:
- Nghiên cứu kiến trúc cloud phù hợp cho sản phẩm
- Thiết kế sơ bộ kiến trúc hệ thống trên AWS
- Tham khảo ý kiến mentor
- Cập nhật bản thiết kế theo feedback
- Chuẩn bị architecture diagram
- Dự thảo project plan & timeline

---

#### Giai đoạn 3: Xây dựng FE và BE (Tuần 9)

**Mục tiêu**: Xây dựng giao diện người dùng (UI) bằng Vue.js và Xây dựng backend API với Django

**Các nhiệm vụ**:
- Xây dựng các trang xác thực người dùng (Landing Page, Sign Up, Sign In, Verify Email, Forgot Password)
- Tạo giao diện quản lý thông tin cá nhân (Profile Management)
- Xây dựng giao diện Chat
- Xử lý trạng thái lỗi trong giao diện
- Thiết lập Django REST Framework
- Tạo model User Profile
- Xây dựng API Authentication (JWT) sử dụng Amazon Cognito
- Xây dựng API quản lý Profile (GET/PUT)
- Xây dựng API tạo hội thoại & gửi tin nhắn

#### Giai đoạn 4: Thiết lập hạ tầng và triển khai ứng dụng (Tuần 10)

**Mục tiêu**:  Thiết lập hạ tầng AWS bằng Terraform và triển khai lên AWS

**Các nhiệm vụ**:
- Viết Terraform modules cho VPC, subnets, security groups
- Triển khai frontend lên S3 bucket
- Tạo CloudFront distribution cho frontend (S3 + CDN)
- Thiết lập AWS Cognito User Pool và App Client
- Containerize Django backend với Docker
- Thiết lập ECS Fargate cluster với auto-scaling (1-4 tasks)
- Thiết lập API Gateway với JWT Authorizer (Cognito integration)
- Cấu hình Application Load Balancer
- Cấu hình VPC Endpoints
- Cấu hình CORS cho API Gateway và Django
- Thiết lập CloudWatch Logs và Alarms
- Kiểm thử end-to-end authentication flow

---

#### Giai đoạn 5: Tích hợp AI & Cơ sở dữ liệu (Tuần 11)

**Mục tiêu**: Tích hợp AWS Bedrock (Claude 3 Haiku) cho tính năng AI chat và thiết lập database PostgreSQL trên AWS RDS

**Các nhiệm vụ**:
- Thiết lập AWS Bedrock và yêu cầu quyền truy cập model (Claude 3 Haiku)
- Xây dựng Bedrock client hỗ trợ streaming (SSE)
- Tích hợp AI vào Chat API với khả năng sử dụng ngữ cảnh hội thoại (context-aware)
- Thiết lập database PostgreSQL trên AWS RDS (Multi-AZ)
- Tạo database models (UserProfile, Conversation, Message)
- Kiểm thử phản hồi AI dựa trên profile người dùng
- Tối ưu prompt engineering cho lời khuyên dinh dưỡng

---

#### Giai đoạn 6: Thử nghiệm và viết báo cáo (Tuần 12)

**Mục tiêu**: Kiểm thử toàn diện và viết báo cáo dự án

**Các nhiệm vụ**:
- Integration testing cho luồng xác thực (authentication flow)
- End-to-end testing cho chức năng chat
- Load testing và stress testing
- Kiểm tra đa trình duyệt (Chrome, Firefox, Safari, Edge)
- Kiểm thử giao diện responsive trên thiết bị di động (iOS, Android)
- Viết báo cáo dự án




### 4.2 Triển khai kỹ thuật

*Quy trình triển khai*: Dự án được triển khai trong 6 giai đoạn trong 6 tuần, nhằm xây dựng một nền tảng trợ lý dinh dưỡng sử dụng AI hoàn chỉnh.

- Tuần 7 – Nghiên cứu & Lập kế hoạch
- Tuần 8 – Lập kế hoạch Kiến trúc
- Tuần 9 – Phát triển Frontend & Backend
- Tuần 10 – Tích hợp AI & Cơ sở dữ liệu
- Tuần 11 – Thiết lập hạ tầng & Triển khai
- Tuần 12 – Kiểm thử & Tài liệu hóa

*Yêu cầu kỹ thuật*

Triển khai hệ thống sẽ theo từng lớp: Mạng (VPC, Subnets, VPC Endpoints) → Bảo mật (Cognito, IAM, Secrets Manager) → Tính toán (ECS Fargate) → Cân bằng tải (ALB, API Gateway) → Lưu trữ & Cơ sở dữ liệu (S3, RDS PostgreSQL) → Tích hợp AI (Bedrock) → Ghi nhật ký/Giám sát (CloudWatch) → CDN & Tối ưu hóa (CloudFront).

Nền tảng dinh dưỡng AI: Kiến thức thực tế về CloudFront (phân phối Vue.js frontend), S3 (lưu trữ static assets), API Gateway (HTTP API với JWT Authorizer), ECS Fargate (chạy Django backend với auto-scaling 1-4 tasks), RDS PostgreSQL (Multi-AZ, 20GB), Bedrock (Claude 3 Haiku cho AI chat), Cognito (quản lý user authentication), và VPC Endpoints (6 endpoints: Bedrock, Secrets Manager, ECR, CloudWatch, S3). Sử dụng Terraform để quản lý infrastructure as code (ví dụ: VPC endpoints cho Bedrock, ECS task definitions, API Gateway routes). Django REST Framework xử lý business logic và giảm thiểu phụ thuộc vào Lambda. Vue.js + Vite cho ứng dụng web fullstack với real-time streaming.

## 5. Lộ trình và mốc triển khai

## Lịch trình Dự án (6 Tuần)

| Tuần | Giai đoạn                       | Nội dung chính                                                                 |
|------|----------------------------------|---------------------------------------------------------------------------------|
| 7    | Nghiên cứu & Lập kế hoạch        | - Xác định mục tiêu dự án<br>- Xác định user & pain points<br>- Thu thập yêu cầu<br>- Xác định use case chính |
| 8    | Lập kế hoạch Kiến trúc          | - Nghiên cứu kiến trúc AWS<br>- Thiết kế kiến trúc hệ thống<br>- Rà soát với mentor<br>- Hoàn thiện architecture diagram<br>- Dự thảo kế hoạch triển khai |
| 9    | Phát triển FE & BE              | - Xây dựng UI (Landing, Sign Up, Sign In, Verify Email, Forgot Password)<br>- Profile Management UI<br>- UI Chat với xử lý lỗi<br>- Thiết lập Django REST Framework<br>- Model User Profile<br>- API Auth (Cognito + JWT)<br>- API Profile (GET/PUT)<br>- API Chat & Conversation |
| 10   | Hạ tầng & Triển khai            | - Viết Terraform cho VPC, Subnets, Security Groups<br>- Triển khai frontend S3 + CloudFront<br>- Thiết lập Cognito User Pool<br>- Containerize backend<br>- ECS Fargate + Auto-scaling<br>- API Gateway + JWT Authorizer<br>- Cấu hình ALB và VPC Endpoints<br>- Thiết lập CloudWatch Logs & Alarms<br>- Kiểm thử end-to-end |
| 11   | Tích hợp AI & Cơ sở dữ liệu    | - Thiết lập AWS Bedrock & quyền truy cập model<br>- Bedrock client + SSE streaming<br>- Tích hợp AI vào Chat API<br>- Context-aware conversation<br>- Thiết lập PostgreSQL RDS (Multi-AZ)<br>- Database models & migration<br>- Kiểm thử AI theo profile user<br>- Tối ưu prompt engineering |
| 12   | Kiểm thử & Báo cáo              | - Integration testing<br>- End-to-end testing<br>- Load & stress testing<br>- Cross-browser testing<br>- Responsive test (iOS, Android)<br>- Viết báo cáo dự án |



---

## 6. ƯỚC TÍNH NGÂN SÁCH

### 6.1 Chi phí Hạ tầng

#### Chi phí Lặp lại Hàng tháng

| Dịch vụ | Cấu hình | Chi phí/Tháng | Ghi chú |
|---------|--------------|------------|-------|
| **ECS Fargate** | 1-4 tasks, 0.5 vCPU, 1GB RAM | $15-30 | Tự động mở rộng dựa trên tải |
| **RDS PostgreSQL** | db.t3.micro, Multi-AZ, 20GB | $15-25 | Bao gồm sao lưu tự động |
| **API Gateway** | HTTP API, ~1M requests | $3-10 | $1/triệu requests |
| **CloudFront** | ~100GB transfer | $1-5 | 1TB đầu tiên miễn phí |
| **S3** | ~5GB storage, ~10K requests | $1 | Lưu trữ website tĩnh |
| **VPC Endpoints** | 2 endpoints (Bedrock, Secrets) | $7 | $0.01/giờ per endpoint |
| **Secrets Manager** | 2 secrets | $1 | $0.40/secret/tháng |
| **CloudWatch** | Logs, Metrics, Alarms | $5-10 | 5GB miễn phí |
| **Bedrock AI** | Claude 3 Haiku | $2-10 | Giá dựa trên sử dụng |

#### Chi phí Sử dụng AI (Bedrock)

| Mức sử dụng | Messages/Ngày | Input Tokens | Output Tokens | Chi phí/Tháng |
|-------------|--------------|--------------|---------------|------------|
| **Thấp** | 100 | 50K | 100K | $0.40 |
| **Trung bình** | 500 | 250K | 500K | $2.00 |
| **Cao** | 2,000 | 1M | 2M | $8.00 |
| **Rất cao** | 10,000 | 5M | 10M | $40.00 |

**Giá**:
- Đầu vào: $0.00025 per 1K tokens
- Đầu ra: $0.00125 per 1K tokens

### 6.2 Chiến lược Tối ưu hóa Chi phí

#### Tối ưu hóa Ngay lập tức

**1. Các Instances Được Bảo lưu** (-30% chi phí RDS)
- Cam kết 1 năm: Giảm 30%
- Cam kết 3 năm: Giảm 50%
- Áp dụng khi traffic ổn định

**2. Các Chính sách Vòng đời S3** (-50% chi phí lưu trữ)
- Chuyển old logs sang S3 Glacier sau 30 ngày
- Xóa logs sau 90 ngày
- Giảm chi phí lưu trữ
- Commit 3 năm: Giảm 50%
- Áp dụng khi traffic ổn định

**2. S3 Lifecycle Policies** (-50% storage cost)
- Chuyển old logs sang S3 Glacier sau 30 ngày
- Delete logs sau 90 ngày
- Giảm storage cost

---

## 7. ĐÁNH GIÁ RỦI RO

### 7.1 Ma trận rủi ro

| Rủi ro                        | Xác suất | Ảnh hưởng | Mức độ nghiêm trọng | Giải pháp giảm thiểu |
|-------------------------------|----------|-----------|---------------------|-----------------------|
| Sự cố dịch vụ AWS             | Thấp     | Cao       | Trung bình         | Triển khai Multi-AZ, thiết lập giám sát |
| Lỗi cơ sở dữ liệu             | Thấp     | Cao       | Trung bình         | RDS Multi-AZ, sao lưu tự động |
| Rủi ro bảo mật                | Thấp     | Rất cao   | Cao                | Tầng bảo mật nhiều lớp, mã hóa dữ liệu |
| Vượt ngân sách                | Trung bình | Trung bình | Trung bình         | Thiết lập CloudWatch billing alarms, giới hạn ngân sách |
| Vấn đề hiệu năng              | Trung bình | Trung bình | Trung bình         | Load testing, auto-scaling |
| Mất dữ liệu                   | Thấp     | Rất cao   | Cao                | Sao lưu tự động, Point-in-time Recovery |

**Thang đánh giá mức độ nghiêm trọng**

- Thấp: Ảnh hưởng nhỏ, dễ xử lý
- Trung bình: Ảnh hưởng trung bình, cần theo dõi và xử lý
- Cao: Ảnh hưởng nghiêm trọng, cần hành động ngay

### 7.2 Chiến lược Giảm thiểu Rủi ro

#### Rủi ro kỹ thuật

**1. Sự cố dịch vụ AWS**

- **Giải pháp giảm thiểu**:
  - Triển khai Multi-AZ cho RDS và ECS
  - Thiết lập CloudWatch alarms theo dõi tình trạng dịch vụ
  - Kích hoạt failover tự động

**2. Lỗi cơ sở dữ liệu**

- **Giải pháp giảm thiểu**:
  - Sử dụng RDS Multi-AZ với failover tự động
  - Hỗ trợ khôi phục Point-in-time (7 ngày)
  - Snapshot database trước mỗi lần triển khai

**3. Rủi ro bảo mật**

- **Giải pháp giảm thiểu**:
  - Áp dụng nhiều lớp bảo mật (API Gateway, Django, VPC)
  - Mã hóa dữ liệu khi lưu trữ và khi truyền tải
  - Thực hiện kiểm tra bảo mật định kỳ
  - CloudTrail để lưu trữ và kiểm tra nhật ký hoạt động

**4. Suy giảm hiệu năng**

- **Giải pháp giảm thiểu**:
  - Thiết lập auto-scaling cho ECS tasks (1-4 tasks)
  - CloudWatch alarms cho CPU/memory cao
  - Load testing trước khi ra mắt
  - CDN caching cho static assets
  - Tối ưu truy vấn cơ sở dữ liệu

#### Rủi ro kinh doanh

**1. Vượt ngân sách**

- **Giải pháp giảm thiểu**:
  - Thiết lập CloudWatch billing alarms
  - Cấu hình AWS Budget alerts
  - Rà soát chi phí hàng tháng
  - Dùng Reserved Instances khi traffic ổn định
  - Thực hiện phân tích và tối ưu chi phí định kỳ

**2. Ít người dùng tiếp cận**

- **Giải pháp giảm thiểu**:
  - Ra mắt MVP với tính năng cốt lõi
  - Thu thập phản hồi người dùng
  - Cải tiến liên tục theo vòng lặp
  - Thực hiện chiến dịch marketing đơn giản
  - Có free tier để thu hút người dùng

**3. Chất lượng AI chưa tốt**

- **Giải pháp giảm thiểu**:
  - Tối ưu prompt engineering và kiểm thử
  - Cơ chế phản hồi từ người dùng
  - A/B testing với nhiều dạng prompt khác nhau
  - Fallback sang hỗ trợ thủ công khi cần thiết
  - Cải tiến liên tục

### 7.3 Kế hoạch Dự phòng

#### Kế hoạch A: Hoạt động bình thường

- Tất cả dịch vụ hoạt động ổn định
- Auto-scaling xử lý tải
- Hệ thống cảnh báo hoạt động tốt

#### Kế hoạch B: Lượng truy cập cao

**Kích hoạt khi**: > 500 người dùng đồng thời
- Tăng số lượng ECS task
- Nâng cấp RDS
- Bật chế độ cache mạnh trên CloudFront

#### Kế hoạch C: Suy giảm dịch vụ

**Kích hoạt khi**: Dịch vụ AWS gặp sự cố
- Kích hoạt Multi-AZ failover
- Chuyển traffic sang AZ hoạt động tốt
- Hiển thị trang trạng thái hệ thống

#### Kế hoạch D: Ngừng hoạt động toàn bộ

**Kích hoạt khi**: Sự cố AWS cấp vùng
- Kích hoạt kế hoạch khôi phục thảm họa
- Khôi phục từ sao lưu
- Triển khai sang region khác

#### Kế hoạch F: Vượt ngân sách

**Kích hoạt khi**: Chi phí > ngân sách
- Rà soát và tối ưu tài nguyên
- Giảm số lượng ECS tasks
- Tắt tính năng không thiết yếu
- Áp dụng rate limiting nghiêm ngặt

---

## 8. KẾT QUẢ DỰ KIẾN

### 8.1 Cải tiến kỹ thuật

#### Các chỉ số hiệu năng

**Tính sẵn sàng**

- Mục tiêu: 99.9% uptime (tối đa 43 phút downtime/tháng)
- Triển khai Multi-AZ
- Tự động failover
- Kiểm tra sức khỏe
- Giảm thời gian phản hồi

**Khả năng mở rộng**

- Auto-scaling: 1-4 ECS tasks
- Hỗ trợ 1.000 người dùng đồng thời
- 10.000 request/phút
- 100 kết nối database đồng thời

**Bảo mật**

- Không ghi nhận sự cố bảo mật
- 100% traffic HTTPS
- Mã hóa dữ liệu khi lưu trữ và truyền tải

### 8.2 Giá trị dài hạn

#### Giá trị kỹ thuật

**Hạ tầng có thể tái sử dụng**

- Các module Terraform dùng lại cho dự án khác
- Template pipeline CI/CD
- Template hệ thống giám sát
- Bộ thực hành bảo mật tốt

**Tài liệu kiến thức**

- Mẫu kiến trúc AWS
- Kinh nghiệm tích hợp AI
- Bài học tối ưu hiệu suất
- Chiến lược tối ưu chi phí

**Kỹ năng đội ngũ**

- Thành thạo AWS
- Tích hợp AI/ML vào sản phẩm
- Kinh nghiệm xây dựng web hiện đại

#### Giá trị chiến lược

**Nền tảng phát triển tiếp**

- Có thể mở rộng thành:
  - Dịch vụ lập kế hoạch bữa ăn
  - Marketplace công thức nấu ăn
  - Ứng dụng theo dõi thể hình
  - Tích hợp khám bệnh từ xa

**Tài sản dữ liệu**

- Sở thích dinh dưỡng của người dùng
- Những món ăn được hỏi nhiều nhất
- Kế hoạch ăn uống hiệu quả
- Insight thị trường

---

## 9. KẾT LUẬN

### 9.1 Tóm tắt

**Về kỹ thuật**

- Kiến trúc cloud-native hiện đại
- Đảm bảo tính sẵn sàng và khả năng mở rộng cao
- Tuân thủ các tiêu chuẩn bảo mật
- Sẵn sàng triển khai sản phẩm thực tế

**Về kinh doanh**

- Giảm chi phí vận hành
- Mô hình kinh doanh dễ mở rộng

**Giá trị cho người dùng**

- Tư vấn dinh dưỡng AI
- Gợi ý cá nhân hóa theo hồ sơ dinh dưỡng
- Giao diện đơn giản, dễ sử dụng, dễ tiếp cận

[linkdocs: proposal docs](https://docs.google.com/document/d/1RizCyvUpP3ky2ArXRSVLJz6_Un53U6i0v0AGytwrcvA/edit?usp=sharing) 
