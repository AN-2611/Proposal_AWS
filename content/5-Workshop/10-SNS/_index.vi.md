
+++
title = "Tạo SNS topic"
date = 2022
weight = 11
chapter = false
pre = "<b>10. </b>"
+++
### Giới thiệu
![iconASG](/images/10-SNS/icon.png)

**Amazon SNS (Simple Notification Service)** là một dịch vụ nhắn tin linh hoạt và được quản lý hoàn toàn để gửi thông báo. Nó hoạt động theo mô hình xuất bản/đăng ký (pub/sub).

Hãy coi Chủ đề SNS như một kênh liên lạc trung tâm hoặc một trung tâm thông báo. Các dịch vụ AWS khác, như CloudWatch, có thể "xuất bản" một tin nhắn (một cảnh báo) đến chủ đề này. Sau đó, SNS ngay lập tức gửi tin nhắn đó đến tất cả các "người đăng ký" của chủ đề.

Người đăng ký có thể là bất cứ thứ gì từ địa chỉ email và số điện thoại di động (SMS) đến các dịch vụ AWS khác như hàm Lambda hoặc hàng đợi SQS. Trong bước này, chúng ta sẽ tạo một chủ đề có tên **alb-alerts** và đăng ký một địa chỉ email vào đó, để bạn có thể nhận các thông báo quan trọng trực tiếp trong hộp thư đến của mình.

### Chi phí
- [Giá Amazon SNS](https://aws.amazon.com/sns/pricing/)

### Tài liệu
- [Amazon SNS](https://docs.aws.amazon.com/sns/)
### Nội dung
1. [Tạo SNS topic](10-SNS/10.1-CreateSNSTopic)
2. [Thêm đăng ký email của bạn](10-SNS/10.2-AddEmail)
