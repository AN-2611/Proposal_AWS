+++
title = "Create Target Groups"
date = 2022
weight = 6
chapter = false
pre = "<b>6.1 </b>"
+++

1. First, navigate to the **EC2 dashboard**. In the left menu, scroll down to **Load Balancing** and click on **Target Groups.**
![EC2 Dashboard](/images/6-TargetGroup/6.1-WebTG/01-EC2Dashboard.png)
1. **Choose a target type:** Select **Instances**.
- Basic configuration:

    - **Target group name:** `web-tg`
    - **Protocol / Port:** HTTP / 80
    - **VPC:**  **alb-advanced-vpc**
    - **Protocol version:** HTTP1
![EC2 Dashboard](/images/6-TargetGroup/6.1-WebTG/02-BasicConfig.png)
- Health checks:
    - **Health check protocol:** HTTP

    - **Health check path:** /

    - Click **Advanced health check settings:**

      - **Healthy threshold:** 2 (An instance is healthy after 2 consecutive successful checks).

      - **Interval:** 15 seconds (Time between checks).
![Health Check](/images/6-TargetGroup/6.1-WebTG/03-HealthCheck-1.png)
1. Click **Next**. On the Register targets page, do not select any instances for now. We will launch and register them later.
2. Click **Create target group.**
3. Repeat the creation process above for the other two target groups, using the specific settings below. All other settings (like VPC, target type, and advanced health checks) can remain the same.
   - API Target Group (`api-tg`):
        - **Target group name:** api-tg
        - **Port:** 8080
        - **Health check path:** /api/health
   - WebSocket Target Group (`websocket-tg`):
        - **Target group name:** websocket-tg
        - **Port:** 3000
        - **Health check path:** /ws/health
4. After all, you have 3 target groups:
![Final result](/images/6-TargetGroup/6.1-WebTG/04-Result.png)