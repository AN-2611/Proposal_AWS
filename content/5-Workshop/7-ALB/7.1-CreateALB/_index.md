+++
title = "Create ALB"
date = 2022
weight = 2
chapter = false
pre = "<b>7.1 </b>"
+++
First, navigate to the **EC2 dashboard**. In the left menu, under **Load Balancing**, click **Load Balancers.**
![EC2 Dashboard](/images/7-ALB/7.1-CreateALB/01-EC2Dashboard.png)
1. Click the **Create Load Balancer button**.
2. From the options, find Application Load Balancer and click Create.
![EC2 Dashboard](/images/7-ALB/7.1-CreateALB/02-ChooseALB.png)
3. Basic Settings:
   - **Load balancer name:** `advanced-alb`
   - **Scheme:** Choose Internet-facing to make it accessible from the internet.
   - **IP address type:** Select IPv4.
![Basic config](/images/7-ALB/7.1-CreateALB/03-BasicConfig.png)
4. Set Up Network Mapping:
   - **VPC:** Select your **advanced-alb-vpc** from the dropdown menu.

   - **Mappings:** In the subnets table, check the boxes for your two public subnets (**public-subnet-1a** and **public-subnet-1b**). The ALB must reside in public subnets to be reachable from the internet.

   - **Security groups:** Uncheck the default security group and select the **alb-sg** you created earlier.
![Network option](/images/7-ALB/7.1-CreateALB/04-Networking.png)
5. Configure Listeners and Routing:
This section defines how the ALB handles incoming traffic on different ports.
- Listeners and routing:
  - For the **Default action**, select **web-tg** from the dropdown.
  - Configure the redirect:
    - **Redirect to:** HTTPS
    - **Port:** 443
![Network option](/images/7-ALB/7.1-CreateALB/05-Listen+Routing.png)
6. Default SSL/TLS server certificate:
   - **Certificate source:** From ACM
   - **Certificate (from ACM):** test.name.vn
   - Choose **Create load balancer** to complete.
![ACMCert](/images/7-ALB/7.1-CreateALB/06-ACMCert.png)
7. Come back to **Load Balancer** you created previously. In **Listeners and rules** tab, choose **Add listener**
![ALB DashBoard](/images/7-ALB/7.1-CreateALB/07-ALBDashBoard.png)
- In **Default action** section:
   - **Routing action**: Redirect to URL
   - **Protocol**: HTTPS
   - **Port**: 443
   - Choose **Add listener** 
![Add Listener HTTPS](/images/7-ALB/7.1-CreateALB/08-AddListenerHTTPS.png)
8. Once complete, you have 2 listener:    
   - HTTP:80 → Redirect to HTTPS
   - HTTPS:443 → Forward to **web-tg**
![Result](/images/7-ALB/7.1-CreateALB/09-Result4.png)