---
title : "Create and Configure Route Tables"
date : "2025-10-10"
weight : 5
chapter : false
pre : " <b> 3.1.4 </b> "
---

### Overall
Route Tables are important components that help route network traffic from Subnets in VPC to different destinations such as Internet Gateway or NAT Gateway. Below are the detailed steps to create and configure Route Tables for Public and Private Subnets.

1. In the VPC dashboard, go to **Route Tables.**
2. Click **Create route table.**
   - **Name:** `public-rt    `
   - **VPC:** Select `advanced-alb-vpc`
   - Click **Create route table.**
![VPC Dashboard](/images/3-VPCSetup/3.1-CreateVPC/3.1.4-CreateRouteTable/01-ConfigRT.png)
3. In the details pane below, select the **Routes tab** and click **Edit routes.**
![Configure route](/images/3-VPCSetup/3.1-CreateVPC/3.1.4-CreateRouteTable/02-EditRoute.png)
4. Click **Add route.**
   - **Destination:** 0.0.0.0/0
   - **Target:** Select Internet Gateway, then choose your `advanced-alb-igw`
   - Select **Save changes**
![Add route](/images/3-VPCSetup/3.1-CreateVPC/3.1.4-CreateRouteTable/03-AddRoute.png)
5. Now, select the **Subnet associations tab** and click **Edit subnet associations.**
![Configure route](/images/3-VPCSetup/3.1-CreateVPC/3.1.4-CreateRouteTable/04-SubnetAssociation.png)
6. Check the boxes for your two public subnets **public-subnet-1a** and **public-subnet-1b**
7. Click **Save associations.**
![Add route](/images/3-VPCSetup/3.1-CreateVPC/3.1.4-CreateRouteTable/05-EditSubnetAssociate.png)
8. Go back to **Route Tables** and click **Create route table.**
   - **Name:** `private-rt    `
   - **VPC:**   `advanced-alb-vpc `
   - Click **Create route table.**
![Add route](/images/3-VPCSetup/3.1-CreateVPC/3.1.4-CreateRouteTable/06-ConfigPrivateRT.png)
9. In the details pane, select the **Routes tab** and click **Edit routes.**
10. Click **Add routes**
    - **Destination**: 0.0.0.0/0
    - **Target**:  NAT Gateway, then choose your **advanced-alb-nat**
    - Click **Save changes.**
![Add route](/images/3-VPCSetup/3.1-CreateVPC/3.1.4-CreateRouteTable/07-EditPrivateRT.png)
11.  Select the **Subnet associations tab** and click **Edit subnet associations.**
![Add route](/images/3-VPCSetup/3.1-CreateVPC/3.1.4-CreateRouteTable/08-PrivateRTAssociate.png)
12.   Check the boxes for your two private subnets **private-subnet-1a** and **private-subnet-1b**
2.   Click **Save associations.**
![Edit RT associate](/images/3-VPCSetup/3.1-CreateVPC/3.1.4-CreateRouteTable/09-EditPrivateRTAssociate.png)