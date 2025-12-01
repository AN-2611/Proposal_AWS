---
title : " Create NAT Gateway"
date : "2025-10-10"
weight : 4
chapter : false
pre : " <b> 3.1.3. </b> "
---
The NAT Gateway allows instances in private subnets to initiate outbound traffic to the internet while remaining private.

1. In the VPC dashboard, go to NAT Gateways.
2. Click **Create NAT gateway.**
![VPC Dashboard](/images/3-VPCSetup/3.1-CreateVPC/3.1.3-CreateNATGW/01-VPCDashboard.png)
3. Configuring the following:
   - **Name:** `advanced-alb-nat`
   - **Subnet:** `public-subnet-1a`
   - **Connectivity type:** Public
   - **Elastic IP allocation ID:**  Click **Allocate Elastic IP**. This will create and associate a new static public IP address for the NAT Gateway.
   - Click **Create NAT gateway.**
![Configure NAT Gateway](/images/3-VPCSetup/3.1-CreateVPC/3.1.3-CreateNATGW/02-ConfigureNATGW.png)
