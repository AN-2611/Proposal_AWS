+++
title = "Initialize Application Load Balancer"
date = 2022
weight = 7
chapter = false
pre = "<b>7. </b>"
+++

### Introduce
![Target group icon](/images/7-ALB/ALB-3.png)
Elastic Load Balancing automatically distributes your incoming traffic across multiple targets, such as EC2 instances, containers, and IP addresses, in one or more Availability Zones. It monitors the health of its registered targets, and routes traffic only to the healthy targets. Elastic Load Balancing scales your load balancer as your incoming traffic changes over time. It can automatically scale to the vast majority of workloads.

In this implementation, the ALB will perform several critical functions:
- **Public Entry Point:** It provides a single, stable DNS name for users to access your application.
- **Traffic Distribution:** It distributes incoming requests across multiple backend servers to ensure no single server is overwhelmed.
- **SSL/TLS Offloading:** It handles the complexity of encrypting and decrypting HTTPS traffic, freeing up your backend servers to focus on their core tasks.
- **Security Enhancement:** By redirecting all unencrypted HTTP traffic to encrypted HTTPS, it ensures secure communication.
- **Modern Protocols:** It natively supports HTTP/2, offering performance improvements like multiplexing and header compression.

### Cost
- [ALB Pricing](https://aws.amazon.com/elasticloadbalancing/pricing/)

### Documentation
- [Application Load Balancers](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/application-load-balancers.html)
- [Enable access logs for your Application Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/enable-access-logging.html)
- [AWS JSON policy elements: Principal](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_principal.html#principal-services)
### Content
1. [Create ALB](7-ALB/7.1-CreateALB)
2. [ Enable Access Logs feature](7-ALB/7.2-EnableAccessLogs)
3. [Configure Routing Rules](7-ALB/7.3-ConfigRoutingRules)
4. [Enable Sticky Sessions](7-ALB/7.4-EnableStickySessions)