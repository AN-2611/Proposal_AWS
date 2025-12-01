---
title : "Create Security groups"
date : "2025-10-10"
weight : 2
chapter : false
pre : " <b> 3.2 </b> "
---
**Security groups** act as stateful virtual firewalls for your resources, controlling all inbound and outbound traffic. The setup below implements a layered security model, which is a crucial best practice.
In this setup, we create a layered security model:

  - Principle of Least Privilege: We only open the exact ports needed. The Application Load Balancer (ALB) is the only component exposed to the internet.

  - Secure Backend: The backend services (Web, API, WebSocket) are completely isolated from the public internet. They are configured to only accept traffic that originates from the ALB's security group. This ensures all requests are properly routed and inspected by the load balancer before reaching your application code.



### Content
1. [Create ALB Security group](/3-VPCSetup/3.2-CreateSecurityGroup/3.2.1-ALBSG)
2. [Create WebSerivce Security group](/3-VPCSetup/3.2-CreateSecurityGroup/3.2.2-WebServiceSG)
3. [Create APIService Security group](/3-VPCSetup/3.2-CreateSecurityGroup/3.2.3-APIServiceSG)
4. [Create WebSocketService Security group](/3-VPCSetup/3.2-CreateSecurityGroup/3.2.4-WebSockerServiceSG)