+++
title = "Clean Resources"
date = 2022
weight = 17
chapter = false
pre = "<b>16. </b>"
+++
1. Go to **VPC > Internet gateways**. Choose **Detach from VPC**
![Delete IGW ](/images/16-CleanResources/01-IGW.png)
2. Scroll down to **NAT Gateways**. Choose **Delete NAT Gateway**
![Delete IGW ](/images/16-CleanResources/02-NAT.png)
3. Go to **Subnets**. Check the boxes for all of subnets. Choose **Delete subnets**
![Delete IGW ](/images/16-CleanResources/03-Subnet.png)
4. Go to **Route tables**. Check the boxes for **public-rt** and **private-rt**. Choose **Delete route tables**
![Delete IGW ](/images/16-CleanResources/04-RT.png)
5. Go to **VPC**. Check the box for **advanced-alb-vpc**. Choose **Delete VPC**
![Delete IGW ](/images/16-CleanResources/05-VPC.png)
6. Go to **Security groups**. Check the boxes for security groups. Choose **Delete security groups**
![Delete IGW ](/images/16-CleanResources/06-SG.png)
7. Navigate to EC2 Dashboard, scroll down to **Auto Scaling Groups**. Check the boxes for three ASG. Choose **Delete**
![Delete IGW ](/images/16-CleanResources/07-ASG.png)
8. Continue scroll down to **Load Balancer**. Check the box for **advanced-alb**. Choose **Delete load balancer**
![Delete IGW ](/images/16-CleanResources/08-LBC.png)
9. In **Load balancing** menu. Choose **Target groups**. Check the boxes for all of three target groups. Choose **Delete**
![Delete IGW ](/images/16-CleanResources/09-TG-2.png)
10. In **Network & Security** menu. Choose **Elastic IPs**. Check the box and then choose **Release Elastic IP addresses**
![Delete IGW ](/images/16-CleanResources/10-ElasticIP.png)
11. Navigate to **SNS Dashboard** > **Topics**. Choose **Delete**
![Delete IGW ](/images/16-CleanResources/11-SNS.png)
12. Navigate to **CloudWatch Dashboard** > **All alarms**. Check all of the boxes. Choose **Delete**
![Delete IGW ](/images/16-CleanResources/12-CW.png)
13. Navigate to **Billing and Cost Management** > **Budgets** > **Overview**. Choose **Delete**
![Delete IGW ](/images/16-CleanResources/13-Cost.png)
14. Navigate to **Route 53** > **Hosted zones**. Check the box. Choose **Delete**
![Delete IGW ](/images/16-CleanResources/14-53.png)
15. Navigate to **AWS Certificate Manager Certificates** > **Certificates**. On **More actions** menu, choose **Delete**
![Delete IGW ](/images/16-CleanResources/15-cert.png)