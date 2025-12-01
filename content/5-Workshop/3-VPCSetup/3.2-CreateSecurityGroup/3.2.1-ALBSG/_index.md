---
title : "Create the ALB Security Group"
date : "2025-10-10"
weight : 2
chapter : false
pre : " <b> 3.2.1. </b> "
---
This group allows public web traffic to reach your Application Load Balancer.
1. Navigate to the **EC2 service** in the AWS Console.
2. In the left navigation pane, under Network & Security, click **Security Groups.**
![SG Dashboard](/images/3-VPCSetup/3.2-CreateSecurityGroup/3.2.1-ALBSG/01-SGDashboard.png)
3. Click the **Create security group** button.
4. Configuring the following:
   - **Security group name:**`alb-sg   `
   - **Description:** `Allows public HTTP and HTTPS traffic for the main ALB.`
   - VPC: `advanced-alb-vpc`
![Name, Description, VPC](/images/3-VPCSetup/3.2-CreateSecurityGroup/3.2.1-ALBSG/02-BasicConfig.png)
5. Inbound rules:
   - Click **Add rule**
     - **Type:** HTTP
     - **Source:** Anywhere-IPv4  
   - Click **Add rule** again
     - **Type:** HTTPS
     - **Source:** Anywhere-IPv4  
![Inbound rule](/images/3-VPCSetup/3.2-CreateSecurityGroup/3.2.1-ALBSG/03-ConfigInboundRules.png)
6. Leave the Outbound rules as the default (Allow all traffic).
7. Click **Create security group.**
