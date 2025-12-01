---
title : "Create the WebSocket Service Security Group"
date : "2025-10-10"
weight : 4
chapter : false
pre : " <b> 3.2.4. </b> "
---
This group allows traffic only from the ALB to your WebSocket servers on port 3000.
1. Follow the same steps again.
2. Basic details:
  - **Security group name:** `websocket-sg`
  - **Description:** `Allows traffic from the ALB to WebSocket servers on port 3000.`
  - **VPC:** Select **advanced-alb-vpc**
![Name,VPC, Description](/images/3-VPCSetup/3.2-CreateSecurityGroup/3.2.4-WebSockerServiceSG/01-BasicConfig.png)
3. Inbound rules:
  - Click **Add rule**
    - **Type:** Custom TCP
    - **Port range:** 3000
    - **Source:** Select your **alb-sg** security group from the list.
![Name,VPC, Description](/images/3-VPCSetup/3.2-CreateSecurityGroup/3.2.4-WebSockerServiceSG/02-InboundRule.png)