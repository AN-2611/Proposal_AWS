+++
title = "WebService"
date = 2022
weight = 16
chapter = false
pre = "<b>14.3 </b>"
+++
1. Navigate to EC2 Dashboard, choose **web-server** instance
2. Choose **Connect**
![ec2 dashboard](/images/14-CheckResult/14.3-WebService/01-EC2Dashboard.png)
3. Update all the installed packages on the system.
```bash
sudo yum update -y
sudo yum install -y nginx
```
4. Enable nginx service
```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```
5. Access to **test.name.vn** you will see nginx install successfully
![ec2 dashboard](/images/14-CheckResult/14.3-WebService/02-Result.png)