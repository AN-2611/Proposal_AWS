
---
title : "Khởi tạo S3 Bucket"
date :  "2025-10-10" 
weight : 6
chapter : false
pre : " <b> 5. </b> "
---

![S3 Bucket](/images/5-S3Bucket/s3_image.png)

### Giới thiệu
Amazon S3 (Simple Storage Service) là một dịch vụ lưu trữ đối tượng có độ bền cao và khả năng mở rộng. Hãy hình dung nó như một ổ cứng gần như vô hạn trên đám mây, hoàn hảo để lưu trữ dữ liệu như tài nguyên ứng dụng, sao lưu và quan trọng nhất đối với bước này là nhật ký (logs).

Chúng ta sẽ tạo S3 bucket này để nhận và lưu trữ nhật ký truy cập từ Application Load Balancer (ALB) của chúng ta. Các nhật ký này cực kỳ có giá trị vì chúng ghi lại thông tin chi tiết về mọi yêu cầu được gửi đến bộ cân bằng tải của bạn. Dữ liệu này rất cần thiết để phân tích các mẫu lưu lượng truy cập, khắc phục sự cố ứng dụng và thực hiện kiểm tra bảo mật.

Chúng ta sẽ kích hoạt hai tính năng chính:
- **Versioning**: Tính năng này bảo vệ nhật ký của bạn bằng cách giữ lịch sử đầy đủ của tất cả các đối tượng, ngăn chặn việc ghi đè hoặc xóa nhầm.
- **Bucket Policy**: Đây là một bước bảo mật bắt buộc, cấp quyền rõ ràng cho dịch vụ ALB để ghi các tệp nhật ký vào bucket của bạn.

### Chi phí
- [Giá S3](https://aws.amazon.com/s3/pricing/)

### Tài liệu tham khảo
- [Tài liệu S3](https://docs.aws.amazon.com/s3/)
- [Phiên bản S3 (Versioning)](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Versioning.html)

### Nội dung
1. [Tạo S3 bucket và bật tính năng Versioning](5-S3Bucket/5.1-Versioning)
