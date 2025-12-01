---
title : "Create the API Service Security Group"
date : "2025-10-10"
weight : 4
chapter : false
pre : " <b> 3.2.3. </b> "
---
This group allows traffic only from the ALB to your API servers on port 8080.
1. We do the same for the `web-sg`
2. Basic details:
     - **Security group name:** `api-sg`
     - **Description:** `Allows traffic from the ALB to API servers on port 8080.`
     - **VPC:** Select `advanced-alb-vpc`
   ![Name,VPC, Description](/images/3-VPCSetup/3.2-CreateSecurityGroup/3.2.3-APIServiceSG/01-BasicConfig.png)
3. Inbound rules:
     - Click **Add rule.**
     - **Type:** Custom TCP
     - **Port range:** 8080
     - **Source:** Select your **alb-sg** security group from the list.
4. Click **Create security group.**
   ![Inbound Rule](/images/3-VPCSetup/3.2-CreateSecurityGroup/3.2.3-APIServiceSG/02-InboundRule.png)