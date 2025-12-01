+++
title = "Khởi tạo Auto Scaling Group"
date = 2022
weight = 10
chapter = false
pre = "<b>9. </b>"
+++
### Giới thiệu
![iconASG](/images/9-ASG/icon.png)
Auto Scaling Groups - ASG là cốt lõi của một ứng dụng linh hoạt và có khả năng phục hồi trên AWS. Nhiệm vụ chính của ASG là tự động quản lý số lượng phiên bản EC2 mà ứng dụng của bạn đang chạy. Nó đảm bảo bạn có đủ sức mạnh tính toán để đáp ứng nhu cầu người dùng, mang lại hai lợi ích chính:
- Tính sẵn sàng cao: Nếu một phiên bản trở nên không ổn định hoặc toàn bộ Vùng sẵn sàng (Availability Zone) gặp sự cố, ASG sẽ tự động chấm dứt phiên bản bị lỗi và khởi chạy một phiên bản mới để thay thế, duy trì thời gian hoạt động của ứng dụng của bạn.
- Tính linh hoạt: Nó tự động thêm nhiều máy chủ hơn khi lưu lượng truy cập cao (mở rộng quy mô) và loại bỏ chúng khi lưu lượng truy cập thấp (thu hẹp quy mô). Điều này đảm bảo trải nghiệm người dùng mượt mà đồng thời giúp bạn tiết kiệm chi phí bằng cách chỉ trả tiền cho các tài nguyên bạn thực sự cần.

### Chi phí
- [Giá AWS Auto Scaling](https://aws.amazon.com/autoscaling/pricing/)

### Tài liệu
- [Tự động thay đổi kích thước Amazon EC2](https://docs.aws.amazon.com/autoscaling/)
### Nội dung
1. [Tạo Auto Scaling Group](9-ASG/9.1-CreateASG)