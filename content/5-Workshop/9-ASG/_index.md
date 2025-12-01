+++
title = "Initialize Auto Scaling Group "
date = 2022
weight = 9
chapter = false
pre = "<b>9. </b>"
+++
### Introduce
![iconASG](/images/9-ASG/icon.png)
Auto Scaling Groups (ASGs) are the core of an elastic and resilient application on AWS. An ASG's primary job is to automatically manage the number of EC2 instances your application runs on. It ensures you have the right amount of compute power to match user demand, providing two key benefits:
- High Availability: If an instance becomes unhealthy or an entire Availability Zone goes down, the ASG will automatically terminate the failed instance and launch a new one to replace it, maintaining your application's uptime.
- Elasticity: It automatically adds more servers when traffic is high (scaling out) and removes them when traffic is low (scaling in). This ensures a smooth user experience while saving you money by only paying for the resources you actually need

### Cost
- [AWS Auto Scaling pricing](https://aws.amazon.com/autoscaling/pricing/)

### Documentation
- [Amazon EC2 Auto Scaling](https://docs.aws.amazon.com/autoscaling/)
### Content
1. [Create Auto Scaling Group](9-ASG/9.1-CreateASG)