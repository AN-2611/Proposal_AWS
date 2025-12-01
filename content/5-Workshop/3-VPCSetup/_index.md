---
title : "Network Infrastructure"
date : "2025-10-10"
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

For this lab, you will work within a pre-configured Virtual Private Cloud (VPC). This setup provides the necessary network foundation for our application and load balancer.

#### The environment includes:
- A VPC with a custom IP address range.
- Security Groups act as virtual firewall, configured to allow public web traffic to ALB and then restrict access to our application servers (EC2 instances)
- Two Public Subnets and Two Private Subnets, distributed across two different Availability Zones to ensure high availability.
- Configuring Route Tables to direct traffic from public subnets to the Internet Gateway
and from private subnets to the NAT Gateway.
- An Internet Gateway attached to the VPC to allow communication with the internet.
- Using AWS Certificate Manager (ACM) to request and validate a public SSL/TLS certificate for our domain.

#### Cost:
1. [NAT Gateway:](https://aws.amazon.com/vi/vpc/pricing/) $0.045 per hour.
2. [Public IPv4 Address:](https://aws.amazon.com/vi/vpc/pricing/) $0.005 per hour.

#### References:
1. [VPC Documentation](https://docs.aws.amazon.com/vpc/)
2. [NAT Gateway Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html)
3. [Internet Gateway Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html)
4. [Route Table Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html)
5. [Security group Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html)
### Content
1. [VPC Setup](3.1-CreateVPC/) 
2. [Create Security groups](3.2-CreateSecurityGroup/)