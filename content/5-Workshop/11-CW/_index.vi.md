
+++
title = "Khởi tạo báo động CloudWatch"
date = 2022
weight = 12
chapter = false
pre = "<b>11. </b>"
+++
### Giới thiệu
![iconASG](/images/11-CW/icon.png)
**Amazon CloudWatch** là dịch vụ giám sát và quan sát gốc của AWS. Nó cung cấp cho bạn dữ liệu và thông tin chi tiết có thể hành động để giám sát các ứng dụng của bạn, hiểu các thay đổi hiệu suất trên toàn hệ thống và phản ứng với các vấn đề về tình trạng hoạt động.

Chúng ta sẽ sử dụng hai tính năng chính của CloudWatch:

- Báo động: Một báo động theo dõi một chỉ số duy nhất và thực hiện một hành động khi chỉ số đó vượt quá ngưỡng đã xác định. Đây là biện pháp phòng thủ chủ động của chúng ta, tự động thông báo cho chúng ta thông qua chủ đề SNS **alb-alerts** khi có sự cố xảy ra, chẳng hạn như máy chủ trở nên không lành mạnh hoặc thời gian phản hồi quá cao.

- Bảng điều khiển: Bảng điều khiển là một trang có thể tùy chỉnh trong bảng điều khiển CloudWatch, nơi bạn có thể tạo một chế độ xem hợp nhất, duy nhất về các chỉ số quan trọng nhất của ứng dụng. Điều này cung cấp cho bạn một cái nhìn tổng quan trực quan "trong nháy mắt" về tình trạng và hiệu suất của hệ thống trong thời gian thực.
### Chi phí
- [Giá AWS CloudWatch](https://aws.amazon.com/cloudwatch/pricing/)

### Tài liệu
- [AWS CloudWatch](https://docs.aws.amazon.com/cloudwatch/)

### Nội dung
1. [Tạo báo động máy chủ không lành mạnh](11-CW/11.1-UnhealthyAlarm)
2. [Tạo báo động CPU cao](11-CW/11.2-HighResponseAlarm)
3. [Tạo bảng điều khiển CloudWatch](11-CW/11.3-CreateCloudWatchDashboard)
