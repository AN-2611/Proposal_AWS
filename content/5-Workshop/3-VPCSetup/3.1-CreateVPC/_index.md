---
title : "VPC Setup"
date : "2025-10-10"
weight : 1
chapter : false
pre : " <b> 3.1. </b> "
---
1. In the search bar, type `VPC   ` then choose **VPC** from the result
![Find VPC](/images/3-VPCSetup/3.1-CreateVPC/01-FindVPC.png)
2. In VPC Dashboard, click **Create VPC**
![VPC Dashboard](/images/3-VPCSetup/3.1-CreateVPC/02-VPCDashboard.png)
3. In the **Create VPC** section, configure the following settings:
   - **Resources to create:** Select VPC only.
   - **Name tag:**`advanced-alb-vpc   `
   - **IPv4 CIDR block:**  `10.0.0.0/16  `
4. Click Create VPC.
![Create VPC](/images/3-VPCSetup/3.1-CreateVPC/03-CreateVPC.png)
5. Once created, select your new VPC from the list. Click the **Actions** dropdown and choose **Edit VPC settings.**
![Edit VPC Setting](/images/3-VPCSetup/3.1-CreateVPC/04-EditVPCSettings.png)
6. Check the box for **Enable DNS hostnames** and ensure **Enable DNS resolution** is also checked.
7. Click **Save**
![DNS resol in VPC Setting](/images/3-VPCSetup/3.1-CreateVPC/05-EnableDNSResolution.png)
