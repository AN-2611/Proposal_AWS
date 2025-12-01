+++
title = "Create Target Groups"
date = 2022
weight = 6
chapter = false
pre = "<b>6. </b>"
+++

### Introduce
![Target group icon](/images/6-TargetGroup/icon.png)
A Target Group is a logical grouping of destination resources, such as EC2 instances, that will handle requests. The Application Load Balancer (ALB) doesn't send traffic directly to instances; instead, it routes traffic to a target group, which then distributes it among its registered instances.

Each target group is configured with a specific protocol and port number. Critically, it includes a health check configuration. The ALB uses this health check to continuously monitor the status of each instance in the group. If an instance fails the health check, the ALB stops sending traffic to it and reroutes requests to the remaining healthy instances, ensuring high availability and fault tolerance for your application.

### Documentation
- [Target groups for your Application Load Balancers](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-target-groups.html)