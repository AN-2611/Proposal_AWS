
+++
title = "Dịch vụ Web"
date = 2022
weight = 16
chapter = false
pre = "<b>14.3 </b>"
+++
1. Điều hướng đến Bảng điều khiển EC2, chọn phiên bản **web-server**
2. Chọn **Connect** (Kết nối)
![Bảng điều khiển EC2](/images/14-CheckResult/14.3-WebService/01-EC2Dashboard.png)
3. Cập nhật tất cả các gói đã cài đặt trên hệ thống.
```bash
sudo yum update -y
sudo yum install -y nginx
```
4. Kích hoạt dịch vụ nginx
```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```
5. Truy cập vào **test.name.vn** bạn sẽ thấy nginx đã được cài đặt thành công
![Bảng điều khiển EC2](/images/14-CheckResult/14.3-WebService/02-Result.png)
