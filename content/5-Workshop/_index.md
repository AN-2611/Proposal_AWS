---
title : "Workshop"
date :  "2025-10-10" 
weight : 5 
chapter : false
pre: " <b> 5. </b> "
---
# IMPLEMENTING ADVANCED FEATURES OF AWS APPLICATION LOAD BALANCER

### Overall
This hands-on lab provides a comprehensive, practical guide to implementing and managing the advanced capabilities of the AWS Application Load Balancer (ALB). Participants will move beyond basic load balancing to configure a highly available, performant, and intelligent application delivery solution. By working through real-world scenarios, you will learn to leverage features that are critical for modern, scalable, and resilient applications, including complex routing, protocol support, and operational best practices.

![ConnectPrivate](/images/arc.jpeg) 
### Workflow### Phase 1: Foundational Networking (VPC)
This phase established the isolated network environment for the application.

*   **Create VPC:** A VPC was created with the CIDR block `10.0.0.0/16`.

*   **Create Subnets:** Four subnets were created across two Availability Zones for high availability:
    *   `public-subnet-1a` (`10.0.1.0/24`)
    *   `public-subnet-1b` (`10.0.2.0/24`)
    *   `private-subnet-1a` (`10.0.3.0/24`)
    *   `private-subnet-1b` (`10.0.4.0/24`)

*   **Configure Gateways:** An Internet Gateway was attached to the VPC for public internet access, and a NAT Gateway was placed in a public subnet to allow private instances to access the internet.

*   **Set Up Route Tables:** A public route table was configured to direct traffic through the Internet Gateway, and a private route table was set up to route outbound traffic from private subnets through the NAT Gateway.

### Phase 2: Security & Configuration
This phase focused on securing the environment and preparing for deployments.

*   **Create Security Groups:** Layered security groups were created to control traffic flow:
    *   `alb-sg`: Allows public HTTP (80) and HTTPS (443) traffic.
    *   `web-sg`: Allows traffic only from `alb-sg` on port 80.
    *   `api-sg`: Allows traffic only from `alb-sg` on port 8080.
    *   `websocket-sg`: Allows traffic only from `alb-sg` on port 3000.

*   **Request SSL Certificate:** An SSL certificate for the domain was requested and validated using AWS Certificate Manager (ACM) to enable HTTPS.

*   **Create IAM Role:** An IAM role (`ec2-alb-role`) was created for EC2 instances, granting them permissions to interact with CloudWatch, S3, and SNS without storing credentials.

*   **Create S3 Bucket:** An S3 bucket was created to store the ALB's access logs for auditing and analysis.

### Phase 3: Application & Compute Layer
This phase deployed the application's core components.

*   **Create Target Groups:** Three distinct target groups were created to route traffic to the different microservices, each with a specific health check path:
    *   `web-tg` (Port 80, `/`)
    *   `api-tg` (Port 8080, `/api/health`)
    *   `websocket-tg` (Port 3000, `/ws/health`)

*   **Create Application Load Balancer (ALB):** An internet-facing ALB was created in the public subnets, configured with the `alb-sg` security group and the ACM certificate. Listeners were set up to redirect HTTP to HTTPS and to handle content-based routing.

*   **Enable Advanced ALB Features:**
    *   **Sticky Sessions:** Enabled on `web-tg` for session affinity.
    *   **Access Logs:** Configured to send logs to the S3 bucket.

*   **Create Launch Templates:** Three separate launch templates were created, each with a specific user data script to bootstrap the application:
    *   `web-service-template` (NGINX)
    *   `api-service-template` (Node.js/Express)
    *   `websocket-service-template` (Node.js/WebSocket)

*   **Create Auto Scaling Groups:** Three Auto Scaling Groups were launched in the private subnets, each linked to its corresponding Launch Template and Target Group, configured to maintain a desired count of 2 instances and scale based on CPU utilization.

### Phase 4: Monitoring, DNS & Cost Management
This final phase made the application observable, publicly accessible, and financially monitored.

*   **Configure Monitoring:**
    *   An SNS Topic (`alb-alerts`) was created for notifications.
    *   CloudWatch Alarms were set for key metrics like `RequestCountPerTarget` and `CPUUtilization` to send alerts to the SNS topic.
    *   A CloudWatch Dashboard was built to visualize the health of the ALB, Target Groups, and EC2 instances in real-time.

*   **Configure DNS:** Amazon Route 53 was used to create an A (Alias) record pointing the root domain to the ALB, CNAME record pointing to subdomain, making the application accessible via a friendly URL.

*   **Set Up Cost Monitoring:** AWS Cost Explorer was enabled, and an AWS Budget was created to monitor monthly spending and send alerts if costs approach the defined limit.

### Content
 1. [Introduction ](1-Introduce)
 2. [Preparation](2-Preparation/)
 3. [Network Infrastructure](3-VPCSetup)
 4. [Request SSL Certificate](4-ACM)
 5. [Initalize S3 Bucket](5-S3Bucket)
 6. [Create Target Groups](6-TargetGroup)
 7. [Initalize Application Load Balancer](7-ALB)
 8. [Initalize EC2 Launch Template](8-EC2LaunchTemplates)
 9. [ Initalize Auto Scaling Group](9-ASG)
 10. [Create SNS topic](10-SNS)
 11. [Initialize CloudWatch Alarms](11-CW)
 12. [ Initialize Cost Monitoring](12-Cost)
 13. [Config DNS records](13-ConfigDNS)
 14. [Check result](14-CheckResult)
 15. [ Performance Testing](15-PerformanceTesting)
 16. [ Clean Resources](16-CleanResources)
