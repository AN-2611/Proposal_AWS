---
title : "Create the Web Service Security Group"
date : "2025-10-10"
weight : 3
chapter : false
pre : " <b> 3.2.2. </b> "
---
This group allows traffic only from the ALB to your web servers on port 80.
1. Return to the **Security Groups page** and click **Create security group**
2. Basic details:
     - **Security group name:** `web-sg  `
     - **Description:** `Allows traffic from the ALB to web servers on port 80.`
     - **VPC:** Select **advanced-alb-vpc**
![Name,VPC, Description](/images/3-VPCSetup/3.2-CreateSecurityGroup/3.2.2-WebServiceSG/01-BasicConfig.png)
1. Inbound rules:
   - Click **Add rule** 
     - **Type:** Custom HTTP
     - **Port range:** 80
     - **Source:** typing `alb-sg`. Select your **alb-sg** security group from the list
![Name,VPC, Description](/images/3-VPCSetup/3.2-CreateSecurityGroup/3.2.2-WebServiceSG/02-InboundRule.png)
1. Click **Create Security group**
