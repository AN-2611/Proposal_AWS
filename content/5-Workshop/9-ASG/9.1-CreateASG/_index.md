+++
title = "Create Auto Scaling Group "
date = 2022
weight = 9
chapter = false
pre = "<b>9.1 </b>"
+++
1. Navigate to the EC2 dashboard. In the left menu, scroll to the bottom and click **Auto Scaling Groups**. Click **Create Auto Scaling group**.
![EC2 Dashboard](/images/9-ASG/9.1-CreateASG/01-EC2Dashboard.png)
2. On **Choose launch template** page:
   - **Auto Scaling group name**: `web-service-asg`
   - **Launch template**: `web-service-template`
   - Click **Next**.
![Create Web serive ASG](/images/9-ASG/9.1-CreateASG/02-CreateWebASG.png)
3. Configure Network Settings:
{{% notice tip %}}
Launching instances in private subnets is a security best practice, as they cannot be reached directly from the internet.
{{% /notice %}}
   - **VPC:** advanced-alb-vpc
   - **Availability Zones and subnets:** private-subnet-1a, private-subnet-1b
   - Click **Next**
![Create Web serive ASG](/images/9-ASG/9.1-CreateASG/03-NetworkingASG.png)
4. Attach the Load Balancer:
   - Select **Attach to an existing load balancer**.
   - Choose **Choose from your load balancer target groups.**
   - Select the **web-tg** from the dropdown menu.
   - Under Health checks, keep the box for Enable ELB health checks checked
   - Click **Next**.
![Create Web serive ASG](/images/9-ASG/9.1-CreateASG/04-LoadBalacingASG.png)
5. Configure Group Size and Scaling
   - **Group size:**    
     - **Desired capacity:** 2 (The number of instances to start with).
     - **Minimum capacity:** 1 (The smallest the group can be).
     - **Maximum capacity:** 4 (The largest the group can be).
   - **Scaling policies:**
     - Select **Target tracking scaling policy.**
     - **Metric type:** Average CPU utilization.
     - **Target value:** 70 %.
     - Keep the default cooldown periods. This policy will automatically add instances if the average CPU load across the fleet rises above 70%.
![Create Web serive ASG](/images/9-ASG/9.1-CreateASG/05-ScalingPolicy.png)
6.  Add Tags:
       - **Key:** Name
       - **Value:** web-server
       - Ensure "Tag new instances" is checked
       - Click **Next**.
![Create Web serive ASG](/images/9-ASG/9.1-CreateASG/06-Tags.png)
7. Review and Create:
      - Carefully review all the settings on the final page.
      - Click **Create Auto Scaling group**. The ASG will now begin launching your two desired **web-server** instances.
8. Create the API and WebSocket ASGs:
Now, repeat the process to create the other two ASGs. The steps are identical; you only need to change the **Name**, **Launch Template**, and **Target Group** for each one.
### For the API Service ASG:
   - **Auto Scaling group name:** `api-service-asg`
   - **Launch template:** api-service-template
   - **Target group:** api-tg
   - Keep all other settings the same: private subnets, Desired=2/Min=1/Max=4, CPU scaling at 70%, etc.

### For the WebSocket Service ASG:
   - **Auto Scaling group name:** `websocket-service-asg`
   - **Launch template:** websocket-service-template
   - **Target group:** websocket-tg
   - Keep all other settings the same.
![After create 3 ASG](/images/9-ASG/9.1-CreateASG/07-ResultASG.png)