
+++
title = "Cấu hình Bản ghi DNS"
date = 2022
weight = 14
chapter = false
pre = "<b>13. </b>"
+++
1. Truy cập trang tổng quan **Route 53**. Chọn **Hosted zones** (Vùng lưu trữ).
![Trang tổng quan Route 53](/images/13-ConfigDNS/01-Route53Dashboard.png)
2. Trên trang chi tiết **test.name.vn**. Chọn **Create record** (Tạo bản ghi):
3. Chi tiết bản ghi:
    - **Record name** (Tên bản ghi): Để trống trường này. Điều này có nghĩa là bạn đang tạo một bản ghi cho tên miền gốc (yourdomain.com).
    - **Record type** (Loại bản ghi): A - Định tuyến lưu lượng truy cập đến địa chỉ IPv4 và một số tài nguyên AWS.
    - Bật công tắc chuyển đổi **Alias** (Bí danh).
4. Định tuyến lưu lượng truy cập đến:
    - **Choose endpoint** (Chọn điểm cuối): Chọn **Alias to Application and Classic Load Balancer** (Bí danh đến Bộ cân bằng tải ứng dụng và cổ điển).
    - **Choose Region** (Chọn Khu vực): Chọn khu vực **us-east-1**.
    - **Choose load balancer** (Chọn bộ cân bằng tải): Nhấp vào trường văn bản và **advanced-alb** của bạn sẽ xuất hiện.
![Bảng điều khiển Route 53](/images/13-ConfigDNS/02-CreateRecord.png)
5. Khi vẫn đang ở trong vùng lưu trữ của bạn, nhấp vào **Create record** (Tạo bản ghi) một lần nữa.
    - **Record details** (Chi tiết bản ghi):
        - **Record name** (Tên bản ghi): `ws`
        - **Record type** (Loại bản ghi): CNAME - Định tuyến lưu lượng truy cập đến một tên miền khác.
        - **Value** (Giá trị): Dán tên DNS của Bộ cân bằng tải ứng dụng của bạn vào đây. (Bạn có thể tìm thấy tên này trên trang EC2 > Load Balancers)
        - **TTL (Seconds)** (TTL (Giây)): Để mặc định là 300.
        - **Routing policy** (Chính sách định tuyến): Định tuyến đơn giản.
        - Nhấp vào **Create records** (Tạo bản ghi).
![Bảng điều khiển Route 53](/images/13-ConfigDNS/03-CNAMERecords.png)
