---
title: "Proposal"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 2. </b> "
---

# AWS APPLICATION LOAD BALANCER
## DEPLOYMENT OF ADVANCED FEATURES OF AWS APPLICATION LOAD BALANCER

![ALB](/images/arc.jpeg)

### 1. Executive Summary
This report presents an assessment and proposal for implementing a highly available and secure web system architecture on the AWS platform, deployed in the us-east-1 region.  
The architecture includes the following components: Route 53, Certificate Manager (ACM), Application Load Balancer (ALB), Auto Scaling Group, CloudWatch, S3, and EC2 instances running in private subnets across two Availability Zones.

The goal of this architecture is to build a stable, scalable, cost-efficient, and secure system that supports Web, API, and WebSocket services in a production environment.

### 2. Problem Statement
#### *Current Problems*
In many traditional web systems or on-premises infrastructures, the following issues commonly occur:

- High investment and maintenance costs: Hardware, storage devices, network systems, and technical personnel require significant upfront costs. In addition, maintenance, upgrades, and periodic replacement lead to a higher total cost of ownership (TCO).

- Manual scalability: When traffic surges unexpectedly, scaling infrastructure must be done manually, which is time-consuming and may interrupt services. Many systems over-provision resources for safety, leading to waste.

- Low fault tolerance: A single hardware failure, configuration error, or power outage can disrupt the entire backend. Redundancy and self-healing mechanisms are difficult to implement in traditional physical infrastructures.

- Limited monitoring and troubleshooting: On-premises systems often lack centralized observability tools. Detecting incidents, tracking performance, or analyzing logs requires manual steps, slowing down incident response and resolution.

- Heavy security and compliance workload: Maintaining firewalls, patch management, access control, and data backups must be handled manually, which is error-prone and resource-intensive.

These limitations result in slower software development cycles, higher operational costs, lower reliability, and insufficient flexibility to meet the rapid changes demanded by modern web applications.

#### *Solution*
The proposed solution is to deploy the web application using a **3-tier architecture** on AWS, consisting of:
- **Presentation Layer:** Users access the system through Route 53 and ALB via HTTPS (secured by ACM certificates).
- **Application Layer:** Runs on EC2 instances in private subnets, divided into three service groups: Web, API, and WebSocket.
- **Data & Monitoring Layer:** Stores logs in S3, monitors resources via CloudWatch, and sends alerts through SNS.

Auto Scaling Groups automatically adjust the number of EC2 instances based on load, while CloudWatch Alarms monitor CPU, memory, and network usage to send alerts when thresholds are exceeded.

#### *Benefits and Return on Investment (ROI)*
**Technical benefits:**
- Ensures 99.9% uptime through multi-AZ design.  
- Reduces latency and improves response time using ALB and optimized routing.  
- Increases security by isolating the backend in private subnets.  
- Automatically scales resources with changing workloads, reducing idle costs.  
- Centralized monitoring and proactive alerting.

**Investment effectiveness (ROI):**
- Reduces operational costs by 20–40% compared to fixed infrastructure.  
- Minimizes downtime → improves user experience → increases revenue.  
- Reusable and easily extensible infrastructure for future projects.

### 3. Solution Architecture
#### *AWS Services Used*
- *Route 53*: Manages DNS, routes domain traffic, supports health checks.  
- *ACM (AWS Certificate Manager)*: Issues and automatically renews SSL/TLS certificates for HTTPS.  
- *VPC (Virtual Private Cloud)*: Provides an isolated network environment for the system.  
- *NAT Gateway*: Allows EC2 instances in private subnets to access the internet for updates without exposing public IPs.  
- *IGW*: Connects the VPC to the Internet.  
- *EC2 Instances (App, API, WebSocket)*: Backend compute servers running in private subnets.  
- *Auto Scaling Group*: Automatically adjusts the number of EC2 instances based on workload.  
- *Application Load Balancer (ALB)*: Distributes traffic among EC2 instances for Web/API/WebSocket.  
- *Amazon CloudWatch*: Monitors performance metrics, collects logs, and triggers alarms when incidents occur.  
- *Amazon SNS*: Sends alert notifications via email/SMS.  
- *S3 (Simple Storage Service)*: Stores ALB access logs.

#### *Component Design*
The backend system consists of three main layers:

1. **Network Layer:** Responsible for connectivity, security, and routing between Internet users and internal VPC resources.
   - Key components:
     - *Amazon Route 53*: Provides global DNS, resolving the application domain to the ALB’s IP address in the us-east-1 region. It ensures fast, reliable access and supports cross-region load balancing in future expansions.
     - *Internet Gateway (IGW)*: Allows Internet traffic to enter and leave the VPC, acting as the main gateway between AWS Cloud and end users.
     - *Application Load Balancer (ALB)*: Serves as the single entry point for all external traffic. ALB distributes requests to EC2 backend groups (Web, API, WebSocket) based on request type or path. Integrated with *AWS Certificate Manager (ACM)* for HTTPS encryption, ensuring secure data transmission.
     - *NAT Gateway*: Located in the Public Subnet, it allows EC2 instances in Private Subnets to access the Internet (e.g., for software updates or API calls) without exposing public IPs, enhancing security.

2. **Application Layer:** Focused on business logic processing and service delivery through EC2 instances.
   - Components:
     - *EC2 Instances (Web, API, WebSocket)*: Located in Private Subnets and inaccessible directly from the Internet. Each EC2 group has its own Security Group allowing traffic only from ALB or NAT Gateway.
     - *Auto Scaling Group (ASG)*: Automatically increases or decreases EC2 instance count based on real load (e.g., CPU > 70%), ensuring performance, reducing costs, and improving reliability.

3. **Monitoring & Management Layer:** Handles log collection, performance monitoring, alerting, and data storage for audits and optimization.
   - Components:
     - *Amazon S3*: Receives and stores ALB access logs.
     - *Amazon CloudWatch*: Collects metrics such as EC2 CPU usage, triggers alarms when CPU > 80% or when overload signs appear, and provides dashboards for real-time performance monitoring.
     - *Amazon SNS*: Receives alerts from CloudWatch and sends notifications via email/SMS to the operations team when incidents occur.

#### *Main Operation Flow*
1. Users access the domain routed by Route 53 → redirected to ALB via HTTPS (secured by ACM).  
2. ALB checks the request type and routes it to the appropriate backend EC2 group in the Private Subnet.  
3. EC2 instances process the request and return the result to ALB → ALB sends the response back to the user.  
4. During operation:  
   - ALB sends access logs to S3.  
   - CloudWatch monitors performance and triggers alarms when thresholds are exceeded.  
   - SNS sends alerts to the operations team.  
   - Auto Scaling automatically increases/decreases EC2 instances as needed.  
5. EC2 instances in Private Subnets use NAT Gateway for Internet access (e.g., downloading updates).

### 4. Technical Implementation
#### *Implementation Phases*
1. *Research and architecture design:* Study and design the AWS architecture.  
2. *Cost estimation and feasibility check:* Use AWS Pricing Calculator for cost estimation and adjustments.  
3. *Architecture optimization:* Fine-tune for cost and performance efficiency.  
4. *Development, testing, deployment:* Implement and test the system.  

#### *Technical Requirements*
1. VPC: 1 VPC with 2 AZs (Multi-AZ).  
2. Subnets: 2 Public Subnets, 2 Private Subnets.  
3. Instances: Minimum 3 EC2 (Web, API, WebSocket).  
4. Auto Scaling: Trigger when CPU > 70%.  
5. Monitoring: CloudWatch + SNS alerts.  
6. Logging: ALB Access Logs → S3 bucket.  
7. Traffic Encryption: HTTPS (ACM certificate).

### 5. Timeline & Milestones
- Internship (Month 1–3): 3 months.  
  - Month 1: Learn and practice AWS services.  
  - Month 2: Design architecture, estimate cost, optimize solution.  
  - Month 3: Implement, test, and launch.

### 6. Budget Estimation
You can view the cost estimate on [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=5177a11066447369fbffcd58f36842343e069f71).

#### *Infrastructure Cost*
- Route 53: 2.25 USD/month (1 hosted zone, basic health check inside and outside AWS).  
- S3 Standard: 0.17 USD/month (5 GB, PUT, COPY, POST, LIST 10,000 requests).  
- ACM: 0 USD/month.  
- VPC: 32.89 USD/month (22 working days, 1 NAT Gateway).  
- EC2: 18.18 USD/month (Workloads monthly (Baseline: 2, Peak: 5), instance: t3.micro, pricing: on-demand).  
- SNS: 0 USD/month (1 million requests/month).  
- CloudWatch: 1.80 USD/month (CPU alarm, request count per target).

*Total*: **55.29 USD/month**

### 7. Risk Assessment
#### *Risk Matrix*
| Risk Type              | Level      | Impact      | Description                              |
| ---------------------- | ---------- | ------------ | ---------------------------------------- |
| EC2 failure            | High       | Medium       | Instance failure or connection loss       |
| NAT Gateway failure    | Medium     | High         | Private subnet loses Internet access      |
| ALB overload           | Medium     | High         | Application becomes unresponsive          |
| Security misconfiguration | High   | High         | Data exposure or external attack          |
| Budget overrun         | Medium     | Medium       | Auto Scaling scales out excessively       |

#### *Mitigation Strategies*
- **Multi-AZ Deployment:** Distribute EC2 instances across 2 AZs to reduce downtime.  
- **Auto Scaling Policy:** Limit the maximum number of EC2 instances.  
- **CloudWatch Alarms:** Monitor workload and trigger instant alerts.  
- **Security Review:** Regularly audit Security Groups, IAM policies, and logs.

#### *Contingency Plan*
- **Budget overrun:** Trigger AWS Budgets alarms and scale down non-production resources.  
- **Log overflow:** Move old logs to Glacier or enable automatic log deletion.  

### 8. Expected Outcomes
#### *Technical Improvements*
- Reduced downtime through HA, Multi-AZ, and ALB health checks.  
- Optimized cost via Auto Scaling.  
- Automated monitoring and alerting improve incident response time.

#### *Long-term Value*
- Easily integrates with CI/CD, advanced monitoring, and data pipelines.  
- The architecture can be expanded into a serverless or container-based model in the future.
