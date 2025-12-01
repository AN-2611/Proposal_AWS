---
title: "DevOps on AWS Workshop"
date: "2025-11-17"
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---


# Summary Report: “DevOps on AWS Workshop”

### Event Objectives

- Provide an overview of DevOps culture, mindset, and principles.  
- Introduce AWS-native DevOps services: **CodeCommit, CodeBuild, CodeDeploy, CodePipeline**.  
- Deliver hands-on knowledge on **Infrastructure as Code** using CloudFormation & CDK.  
- Deep-dive into container platforms including **ECR, ECS, EKS, App Runner**.  
- Explore monitoring and observability with **CloudWatch & AWS X-Ray**.  
- Share best practices, deployment strategies, and DevOps career directions.

---

### Agenda Overview

**Time:** 8:30 AM – 5:00 PM, Monday, November 17, 2025  
**Location:** AWS Vietnam Office  

---

## Key Highlights

## Morning Session (8:30 AM – 12:00 PM)

### 1. Welcome & DevOps Mindset (8:30 – 9:00 AM)

- Short recap of the previous AI/ML session.  
- Introduction to DevOps culture and core principles.  
- Benefits of DevOps and key performance metrics:  
  - **DORA Metrics**  
  - **MTTR** (Mean Time to Recovery)  
  - Deployment frequency  

---

### 2. AWS DevOps Services – CI/CD Pipeline (9:00 – 10:30 AM)

The session covered a complete CI/CD pipeline built with AWS-native services.

#### **Source Control**
- **AWS CodeCommit**  
- Git strategies:  
  - GitFlow  
  - Trunk-based development  

#### **Build & Test**
- **AWS CodeBuild**  
- Buildspec configuration  
- Designing automated testing pipelines  

#### **Deployment**
- **AWS CodeDeploy** and deployment strategies:  
  - Blue/Green  
  - Canary  
  - Rolling updates  

#### **Orchestration**
- **AWS CodePipeline** for end-to-end automation  

#### **Live Demo**
- Full CI/CD pipeline walkthrough from commit → build → test → deploy.

---

### 3. Break (10:30 – 10:45 AM)

---

### 4. Infrastructure as Code (IaC) (10:45 AM – 12:00 PM)

#### **AWS CloudFormation**
- Templates, stacks, change sets  
- Drift detection and management  

#### **AWS CDK (Cloud Development Kit)**
- Constructs and reusable patterns  
- Multi-language support: TypeScript, Python, Java, C#  

#### **Live Demo**
- Deploying infrastructure using CloudFormation & CDK  

#### **Discussion**
- When to choose CloudFormation vs CDK  
- Advantages and limitations of each IaC approach  

---

### Lunch Break (12:00 – 1:00 PM)

---

## Afternoon Session (1:00 PM – 5:00 PM)

### 5. Container Services on AWS (1:00 – 2:30 PM)

#### **Docker Fundamentals**
- Microservices architecture  
- Containerization concepts  

#### **Amazon ECR**
- Container image registry  
- Image scanning & security  
- Lifecycle policies  

#### **Amazon ECS & EKS**
- Deployment strategies  
- Auto scaling  
- Key differences:  
  - ECS: AWS-managed  
  - EKS: Kubernetes-native  

#### **AWS App Runner**
- Simplified container deployment  
- Ideal for quick deployments and small services  

#### **Demo & Case Study**
- Comparison of microservices deployment on ECS, EKS, and App Runner.

---

### 6. Break (2:30 – 2:45 PM)

---

### 7. Monitoring & Observability (2:45 – 4:00 PM)

#### **Amazon CloudWatch**
- Metrics  
- Logs  
- Alarms  
- Custom dashboards  

#### **AWS X-Ray**
- Distributed tracing  
- Request flows and performance bottlenecks visibility  

#### **Live Demo**
- Setting up a full-stack observability pipeline  

#### **Best Practices**
- Effective alerting  
- Dashboard design  
- On-call and incident response workflow  

---

### 8. DevOps Best Practices & Case Studies (4:00 – 4:45 PM)

- Deployment strategies:  
  - Feature flags  
  - A/B testing  
- Automated testing integration in CI/CD  
- Incident management & postmortems  
- Case studies from startups and enterprise DevOps transformations  

---

### 9. Q&A & Wrap-up (4:45 – 5:00 PM)

- DevOps career directions and skill roadmap  
- AWS DevOps certification pathways (DVA-C02, DOP-C02)

---

## Key Takeaways

### DevOps Fundamentals
- DevOps is rooted in collaboration, culture, and continuous improvement.  
- Key metrics such as **DORA** and **MTTR** measure DevOps performance effectively.

### CI/CD on AWS
- CodePipeline + CodeBuild + CodeDeploy empower scalable, automated pipelines.  
- CI/CD standardizes delivery and reduces deployment risks.

### IaC Principles
- IaC is essential for modern DevOps workflows.  
- CloudFormation excels in enterprise templates; CDK offers developer-friendly flexibility.

### Container Orchestration
- ECS is simple and fully managed; EKS is powerful for Kubernetes workloads.  
- App Runner is ideal for fast, simplified container deployment.

### Observability
- CloudWatch & X-Ray provide deep visibility across logs, metrics, and traces.  
- Strong observability practices improve system reliability and reduce MTTR.

---

### Some event photos
*Add your event photos here*

---

> The workshop provided a comprehensive journey through modern DevOps practices on AWS — from CI/CD pipelines and IaC to containers and observability. Participants gained both technical knowledge and practical understanding needed to pursue a DevOps career successfully.

