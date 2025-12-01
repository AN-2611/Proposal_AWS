
+++
title = "Dịch vụ WebSocket"
date = 2022
weight = 15
chapter = false
pre = "<b>14.2 </b>"
+++
1. Điều hướng đến Bảng điều khiển EC2, chọn phiên bản **web-server**
2. Chọn **Connect** (Kết nối)
![Bảng điều khiển EC2](/images/14-CheckResult/14.2-WebSocketService/01-EC2Dashboard.png)
3. Cập nhật tất cả các gói đã cài đặt trên hệ thống.
```bash

sudo yum update -y
sudo dnf install -y nodejs
sudo npm install -g pm2
```
4. Tạo thư mục và tệp cho ứng dụng websocket
```bash
sudo mkdir /home/ec2-user/websocket-app
sudo cd /home/ec2-user/websocket-app
```
5. Tạo tệp ứng dụng Node.js với 'WS' và 'Express'
```bash
sudo nano websocket.js
```
6. Dán đoạn mã sau vào nano:
```bash
const express = require('express');
const http = require('http');
const WebSocket = require('ws');

const port = 3000;
const app = express();
const server = http.createServer(app);
const wss = new WebSocket.Server({ server });

wss.on('connection', (ws) => {
  console.log('Client connected');
  ws.on('message', (message) => {
    console.log(`Received message => ${message}`);
    ws.send(`Hello, you sent -> ${message}`);
  });
  ws.send('Hi there, I am a WebSocket server');
});

app.get('/ws/health', (req, res) => {
  res.status(200).send({ status: 'ok' });
});

server.listen(port, () => {
  console.log(`WebSocket service listening on port ${port}`);
});
```
7. Cài đặt các thư viện cần thiết và khởi chạy ứng dụng trong PM2
```bash
sudo npm install express ws 
sudo pm2 start websocket.js
sudo npm install -g wscat
```
8. Kết nối đến máy chủ WebSocket: `wscat -c ws://localhost:3000`
![Bảng điều khiển EC2](/images/14-CheckResult/14.2-WebSocketService/02-Result.png)
