
+++
title = "Dịch vụ API"
date = 2022
weight = 14
chapter = false
pre = "<b>14.1 </b>"
+++
1. Điều hướng đến Bảng điều khiển EC2, chọn phiên bản **api-server**
2. Chọn **Connect** (Kết nối)
![Bảng điều khiển EC2](/images/14-CheckResult/14.1-APIService/01-EC2Dashboard.png)
1. Chọn **Session Manager**. Chọn **Connect** (Kết nối)
![Bảng điều khiển EC2](/images/14-CheckResult/14.1-APIService/02-ConnectEC2.png)
1. Cập nhật hệ thống và cài đặt các gói cần thiết:
```bash
# Cập nhật các gói hệ thống
sudo yum update -y

# Cài đặt Node.js và npm
sudo yum install -y nodejs npm

# Cài đặt trình quản lý tiến trình PM2 toàn cục
sudo npm install pm2
```
5. Tạo thư mục và các tệp cho ứng dụng
```bash
# Tạo thư mục cho dịch vụ API
sudo mkdir -p /opt/api-service
```
6. Tạo một tệp package.json. Chạy lệnh sau để mở trình soạn thảo văn bản nano:
```bash
sudo nano /opt/api-service/package.json
```
7. Dán nội dung sau vào trình soạn thảo, sau đó nhấn **Ctrl+X**, sau đó **Y**, và **Enter** để lưu và thoát.
```json
{
  "name": "api-service",
  "version": "1.0.0",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.18.0"
  }
}
```
8. Hãy tạo một tệp server.js. Chạy lệnh này để mở trình soạn thảo:
```bash
sudo nano /opt/api-service/server.js
```
9. Dán đoạn mã JavaScript sau, sau đó lưu và thoát (Ctrl+X, Y, Enter).
```bash
const express = require('express');
const app = express();
const port = 8080;

app.get('/api/health', (req, res) => {
  res.json({ status: 'healthy', service: 'api', port: 8080 });
});

app.get('/api', (req, res) => {
  res.json({ 
    message: 'API Service Running', 
    server: require('os').hostname()
  });
});

app.listen(port, '0.0.0.0', () => {
  console.log(`API service listening on port ${port}`);
});
```
10. Cài đặt các phụ thuộc:
```bash
# Di chuyển vào thư mục ứng dụng
cd /opt/api-service

# Cài đặt các phụ thuộc của dự án
sudo npm install
```
11. Tạo tệp **api-service.service**
```bash
sudo nano /etc/systemd/system/api-service.service
```
12. Dán đoạn mã JavaScript sau, sau đó lưu và thoát (Ctrl+X, Y, Enter).
```bash
[Unit]
Description=API Service
After=network.target

[Service]
Type=simple
User=ec2-user
WorkingDirectory=/opt/api-service
ExecStart=/usr/bin/node server.js
Restart=always

[Install]
WantedBy=multi-user.target
```
13. Khởi động lại dịch vụ:
```bash
sudo systemctl daemon-reload
sudo systemctl enable api-service
sudo systemctl start api-service
```
14. Kiểm tra trạng thái của dịch vụ:
```bash
sudo systemctl status api-service
```
![Bảng điều khiển EC2](/images/14-CheckResult/14.1-APIService/03-CheckStatus.png)
15. Đây là kết quả khi tôi truy cập vào **test.name.vn/api/** và **test.name.vn/api/health**
![Bảng điều khiển EC2](/images/14-CheckResult/14.1-APIService/04-Resultl.png)
