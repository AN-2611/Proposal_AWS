Tuyệt vời! Đây là bản dịch sang tiếng Anh chuyên ngành điện toán đám mây AWS, giữ nguyên định dạng markdown:

```
+++
title = "WebSocket Service"
date = 2022
weight = 15
chapter = false
pre = "<b>14.2 </b>"
+++
1. Navigate to the EC2 Dashboard, select the **web-server** instance.
2. Choose **Connect**
![EC2 Dashboard](/images/14-CheckResult/14.2-WebSocketService/01-EC2Dashboard.png)
3. Update all installed packages on the system.
```bash

sudo yum update -y
sudo dnf install -y nodejs
sudo npm install -g pm2
```
4. Create directory and files for the websocket application.
```bash
sudo mkdir /home/ec2-user/websocket-app
sudo cd /home/ec2-user/websocket-app
```
5. Create a Node.js application file with 'WS' and 'Express'.
```bash
sudo nano websocket.js
```
6. Paste the following code into nano:
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
7. Install necessary libraries and start the application in PM2.
```bash
sudo npm install express ws 
sudo pm2 start websocket.js
sudo npm install -g wscat
```
8. Connect to the WebSocket server: `wscat -c ws://localhost:3000`
![EC2 Dashboard](/images/14-CheckResult/14.2-WebSocketService/02-Result.png)
```