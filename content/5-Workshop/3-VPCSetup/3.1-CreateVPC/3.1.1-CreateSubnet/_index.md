---
title : "Create subnets"
date : "2025-10-10"
weight : 2
chapter : false
pre : " <b> 3.1.1. </b> "
---
Now, we will create two public and two private subnets across two Availability Zones (AZs).
1. In the VPC dashboard, go to **Subnets** in the left menu.
2. Click **Create subnet**
![VPC Dashboard](/images/3-VPCSetup/3.1-CreateVPC/3.1.1-CreateSubnet/01-SubnetDashboard.png)
3. Select VPC you just created
4. Create the four subnets one by one with the following configurations:
   - Subnet 1 
     - **Subnet name:** `public-subnet-1a`
     - **Availability Zone:** us-east-1a
     - **IPv4 CIDR block:**`10.0.1.0/24`
     - Click **Add new subnet** to configure the next one.
   - Subnet 2
     - **Subnet name:** `public-subnet-1b`
     - **Availability Zone:** us-east-1b
     - **IPv4 CIDR block:** `10.0.2.0/24`
   - Subnet 3
     - **Subnet name:** `private-subnet-1a`
     - **Availability Zone:** us-east-1a
     - **IPv4 CIDR block:** `10.0.3.0/24`
   - Subnet 4
     - **Subnet name:**`private-subnet-1b`
     - **Availability Zone:** us-east-1b
     - **IPv4 CIDR block:**`10.0.4.0/24`
5. After defining all four subnets, click the **Create subnet** button
6. Your subnet create successfully
![Create Subnet Success](/images/3-VPCSetup/3.1-CreateVPC/3.1.1-CreateSubnet/02-CreateSuccess.png)