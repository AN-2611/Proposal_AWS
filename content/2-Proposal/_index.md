---
title: "Proposal"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 1. </b> "
---


# AWS APPLICATION LOAD BALANCER
## DEPLOYING ADVANCED FEATURES OF AWS APPLICATION LOAD BALANCER

![ALB](/images/2-Proposal/arc.jpeg)

### 1. Executive Summary
The business requires a web platform capable of serving thousands of concurrent users, ensuring high security, performance, scalability, and reliability. The proposed solution uses the AWS Cloud with a modern 3-tier architecture, leveraging managed services.

This proposal presents an evaluation of a **Private Architecture** AWS system design intended for deploying a secure, flexible, and high-performance backend environment.
The system operates within a VPC (Virtual Private Cloud), consisting of a public subnet containing a NAT Gateway and private subnets housing the EC2 instances responsible for App, API, and WebSocket services.

This architecture emphasizes network segregation, observability, cost optimization, while maintaining future scalability.

### 2. Problem Statement
*Current Problem*
Traditional backend deployment models (on-premises) face significant limitations in terms of scalability, flexibility, and operational efficiency. In the old architecture, all servers, databases, and network components were deployed on physical infrastructure managed by the internal IT team. This leads to several issues:

High investment and maintenance costs: Purchasing and maintaining servers, storage devices, and network infrastructure requires large initial capital expenditure and ongoing operational costs.

Difficult to scale flexibly: When traffic surges, system expansion requires manual intervention, causing service disruption or leading to over-provisioning of resources.

Complex and error-prone deployment: Configuration, version management, and deployment processes across multiple environments (dev, test, prod) are manual, time-consuming, and prone to errors.

Low fault tolerance: Hardware failures or misconfigurations can bring down the entire backend, as mechanisms for redundancy and automatic recovery are difficult to implement on physical infrastructure.

Difficult to monitor and troubleshoot: Traditional systems often lack integrated observability tools, making performance and security monitoring challenging.

Security and compliance burden: Manually maintaining firewalls, applying patches, and protecting data consumes significant resources and poses potential risks.

These limitations result in slow development cycles, high operating costs, and a lack of the flexibility needed to meet the requirements of modern applications.

*Solution*
To overcome the limitations of the traditional backend deployment model (on-premises), this proposal introduces a **cloud-native backend environment** on the AWS platform.

The solution leverages AWS serverless and managed services to achieve high scalability, robust security, optimized cost, and minimal operational complexity.

*Benefits and Return on Investment (ROI)*
- Enhanced scalability and availability: Managed AWS services allow for near-limitless scaling without manual intervention, and the Multi-AZ design ensures fault tolerance and minimizes service downtime.

- Security and compliance: Implementing IAM, Security Groups, and data encryption protects the entire backend system. AWS complies with numerous international standards (ISO, SOC, GDPR...), facilitating the company's security certification process.

- Cost Efficiency: Reduced initial investment costs, optimized operational expenditure, and automatic scaling adjusts resources according to the load, preventing waste from over-provisioning.

- Better observability and monitoring: Using CloudWatch for monitoring, early fault detection, and rapid troubleshooting.

- Flexibility: The architecture is adaptable for future expansion into microservices or containers.

### 3. Solution Architecture
Main Flow: <br>
User → DNS (Route 53) → ALB. <br>
ALB (HTTPS termination using ACM) → distributes load to Web/API/WebSocket instances in private subnets. <br>
Instances run in Auto Scaling Groups across AZs, health-checked by ALB.<br>
Outbound traffic (updates, API calls) goes through NAT Gateway.<br>
Logs from ALB → S3, metrics from EC2/ALB → CloudWatch.<br>
CloudWatch alarms → SNS → notify Ops team. <br>


*AWS Services Used*
- *VPC (Virtual Private Cloud)*: Creates a private network environment for the entire backend system.
- *Subnets (Public & Private)*: Separates public resources (NAT) from private resources (App, API, WebSocket).
- *NAT Gateway*: Allows backend instances in the private subnet to securely access the Internet without exposing their IP addresses.
- *EC2 Instances (App, API, WebSocket)*: Hosts and runs core backend services such as business logic, REST APIs, and real-time WebSocket connections.
- *Application Load Balancer (ALB)*: Balances load across backend instances, ensuring availability and stable performance.
- *Auto Scaling Group*: Automatically scales the number of EC2 instances up or down based on system load.
- *Amazon CloudWatch*: Monitors performance, collects logs, and sends alerts upon incidents.
- *Amazon SNS*: Automatically sends notifications upon detection of critical events or system failures.
- *Security Groups*: Controls inbound/outbound network traffic to protect backend resources.

*Component Design*

The backend system consists of three main layers:
1. Network Layer
- The VPC is divided into Public and Private subnets.
- The Public subnet only contains the NAT Gateway, allowing the backend to access the Internet for updates or external API calls.
- The Private subnet contains the App, API, and WebSocket services, ensuring they are not directly accessible from the outside.

1. Application Layer
- App Service: Handles core business logic, interacting with internal APIs.
- API Service: Receives and processes requests from the frontend or other systems via the Application Load Balancer (ALB).
- WebSocket Service: Provides real-time, bidirectional communication.
- ALB: Balances load across instances, reducing downtime and increasing reliability.

1. Monitoring & Management Layer
- CloudWatch: Monitors logs and system performance, sends automatic alerts.
- SNS: Notifies the admin team of critical errors.
- Auto Scaling: Automatically scales EC2 resources up or down to optimize cost and performance.


### 4. Technical Deployment
*Deployment Phases*
1. *Research and Architecture Design*: Research and design the AWS architecture.
2. *Cost Estimation and Feasibility Check*: Use the AWS Pricing Calculator for estimation and adjustment.
3. *Architecture Refinement for Cost/Solution Optimization*: Fine-tuning to ensure efficiency.
4. *Development, Testing, Deployment*: System implementation.

*Technical Requirements*
- *System deployment will be layered*: Network layer -> Security layer -> Compute & Application layer -> Scalability & Availability layer -> Storage & Data layer -> Monitoring & Logging layer.


### 5. Roadmap & Deployment Milestones
- Internship Period (Months 1-3): 3 months.
    - Month 1: Research, learn to use AWS services.
    - Month 2: Research, design, cost estimation, architectural refinement.
    - Month 3: Implementation, testing, launch.

### 6. Budget Estimation
The cost can be viewed on the [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=621f38b12a1ef026842ba2ddfe46ff936ed4ab01)
Or download the [budget estimation file](../attachments/budget_estimation.pdf).

*Infrastructure Costs*
- AWS Lambda: 0.00 USD/month (1,000 requests, 512 MB storage).
- S3 Standard: 0.15 USD/month (6 GB, 2,100 requests, 1 GB scan).
- Data Transfer: 0.02 USD/month (1 GB in, 1 GB out).
- AWS Amplify: 0.35 USD/month (256 MB, 500 ms request).
- Amazon API Gateway: 0.01 USD/month (2,000 requests).
- AWS Glue ETL Jobs: 0.02 USD/month (2 DPU).
- AWS Glue Crawlers: 0.07 USD/month (1 crawler).
- MQTT (IoT Core): 0.08 USD/month (5 devices, 45,000 messages).

*Total*: 0.7 USD/month, 8.40 USD/12 months
- *Hardware*: 265 USD one-time (Raspberry Pi 5 and sensors).

### 7. Risk Assessment
*Risk Matrix*
- Log growth too fast: Medium impact, Medium probability.
- Exceeding budget: Medium impact, Low probability.

*Mitigation Strategy*
- Log/Data growth: Archive old logs to S3 Glacier.
- Cost: AWS budget alerts, service optimization.

*Contingency Plan*
- Cost threshold exceeded → Trigger AWS Budgets alarm, scale down non-prod resources.
- Logs full → Transfer logs to Glacier or automatically delete old logs.

### 8. Expected Outcomes
*Downtime*: Reduced thanks to HA, multi-AZ, ALB health check.
*Cost*: Cost optimization of 20–30% thanks to auto scaling + logs lifecycle.