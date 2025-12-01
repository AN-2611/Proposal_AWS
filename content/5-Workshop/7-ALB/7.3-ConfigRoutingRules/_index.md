+++
title = "Configure Routing Rules"
date = 2022
weight = 4
chapter = false
pre = "<b>7.3 </b>"
+++
1. Go back to Load Balancer detail: **advanced-alb**. 
   - Choose tick box **HTTPS:443**
   - Choose **Manage rules** from dropdown
   - Choose **Edit rule**
![EC2 Dashboard](/images/7-ALB/7.3-ConfigRoutingRules/01-ALBDashboard.png)
   - Choose **Add rule**
2. In **Add rule** page:
   - Choose **Path** from **Add Conditions**: `/api/*`
   - **Routing action**: Forward to target groups
   - **Target group**: api-tg
   - Choose **Next**
![Add API rule](/images/7-ALB/7.3-ConfigRoutingRules/03-AddAPIRule.png)
1. Continue create another rule:
   - Choose **Host header** from **Add Conditions**: `ws.test.name.vn`
   - **Routing action**: Forward to target groups
   - **Target group**: websocket-tg
   - Choose **Next**
![Add API rule](/images/7-ALB/7.3-ConfigRoutingRules/04-HostHeaderRule.png) 
