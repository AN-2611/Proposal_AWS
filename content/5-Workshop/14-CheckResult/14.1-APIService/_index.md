+++
title = "API Service"
date = 2022
weight = 14
chapter = false
pre = "<b>14.1 </b>"
+++
1. Navigate to EC2 Dashboard, choose **api-server** instance
2. Choose **Connect**
![ec2 dashboard](/images/14-CheckResult/14.1-APIService/01-EC2Dashboard.png)
1. Select **Session Manager**. Choose **Connect**
![ec2 dashboard](/images/14-CheckResult/14.1-APIService/02-ConnectEC2.png)
1. Update the system and install necessary packages:
```bash
# Update system packages
sudo yum update -y

# Install Node.js and npm
sudo yum install -y nodejs npm

# Install PM2 process manager globally
sudo npm install pm2
```
5. Create directory and files for application
```bash
# Create directory for API service
sudo mkdir -p /opt/api-service
```
6. Create a package.json file. Run the following command to open the nano text editor:
```bash
sudo nano /opt/api-service/package.json
```
7. Paste the following into the editor, then press **Ctrl+X**, then **Y**, and **Enter** to save and exit.
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
8. Let's create a server.js file. Run this command to open the editor:
```bash
sudo nano /opt/api-service/server.js
```
9. Paste the following JavaScript code, then save and exit (Ctrl+X, Y, Enter).
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
10. Install dependencies:
```bash
# Move into the application directory
cd /opt/api-service

# Install project dependencies
sudo npm install
```
11. Create **api-service.service** file
```bash
sudo nano /etc/systemd/system/api-service.service
```
12. Paste the following JavaScript code, then save and exit (Ctrl+X, Y, Enter).
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
13. Restart the service: 
```bash
sudo systemctl daemon-reload
sudo systemctl enable api-service
sudo systemctl start api-service
```
14. Check the status of the service:
```bash
sudo systemctl status api-service
```
![ec2 dashboard](/images/14-CheckResult/14.1-APIService/03-CheckStatus.png)
15. This is result when I access to **test.name.vn/api/** and **test.name.vn/api/health**
![ec2 dashboard](/images/14-CheckResult/14.1-APIService/04-Resultl.png)