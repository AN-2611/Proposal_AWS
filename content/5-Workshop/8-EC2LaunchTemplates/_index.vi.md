+++
title = "Khởi tạo Mẫu khởi chạy EC2"
date = 2022
weight = 9
chapter = false
pre = "<b>8. </b>"
+++

### Giới thiệu
![Biểu tượng EC2](/images/8-EC2LaunchTemplates/icon-2.png)
Mẫu khởi chạy EC2 (EC2 Launch Template) là một bản thiết kế cấu hình có thể tái sử dụng, định nghĩa cách khởi chạy một phiên bản EC2. Thay vì phải chỉ định thủ công các cài đặt giống nhau (như AMI, loại phiên bản và nhóm bảo mật) mỗi khi bạn cần một máy chủ mới, bạn chỉ cần định nghĩa chúng một lần trong một mẫu.

Đây là một thực tiễn tốt nhất quan trọng cho tự động hóa và tính nhất quán. Các mẫu khởi chạy là nền tảng cho Nhóm Tự động Thay đổi Kích thước (Auto Scaling Groups), cho phép hệ thống tự động khởi chạy các phiên bản mới, giống hệt nhau đã được cấu hình sẵn và sẵn sàng phục vụ lưu lượng truy cập. Bằng cách sử dụng một mẫu, bạn đảm bảo mọi máy chủ trong đội hình của mình là một bản sao hoàn hảo, giảm lỗi cấu hình và đơn giản hóa việc quản lý.

### Chi phí
- [Giá Amazon EC2](https://aws.amazon.com/ec2/pricing/)

### Tài liệu
- [Tạo mẫu khởi chạy Amazon EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/create-launch-template.html)
- [Lưu trữ các thông số khởi chạy phiên bản trong các mẫu khởi chạy Amazon EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-launch-templates.html)
### Nội dung
1. [Tạo Mẫu khởi chạy EC2](8-EC2LaunchTemplates/8.1-CreateEC2LaunchTemplate)
