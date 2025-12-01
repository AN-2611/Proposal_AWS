---
title: "DevOps on AWS Workshop"
date: "2025-11-17"
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---


# Summary Report: “DevOps on AWS Workshop”

### Event Objectives

- Giới thiệu tổng quan về DevOps trên AWS, bao gồm văn hóa, nguyên tắc và mindset.  
- Trình bày chi tiết các dịch vụ DevOps của AWS: **CodeCommit, CodeBuild, CodeDeploy, CodePipeline**.  
- Hướng dẫn thực hành về **Infrastructure as Code** (CloudFormation & CDK).  
- Cung cấp kiến thức sâu về container services: **ECR, ECS, EKS, App Runner**.  
- Thực hành quan sát hệ thống (Observability) với **CloudWatch & X-Ray**.  
- Tìm hiểu best practices, chiến lược triển khai và lộ trình nghề nghiệp DevOps.

---

### Agenda Overview

**Thời gian:** 8:30 AM – 5:00 PM, Thứ Hai ngày 17/11/2025  
**Địa điểm:** AWS Vietnam Office

---

## Key Highlights

## Morning Session (8:30 AM – 12:00 PM)

### 1. Welcome & DevOps Mindset (8:30 – 9:00 AM)

- Recap nhanh nội dung buổi AI/ML trước đó.  
- Giới thiệu văn hóa DevOps và các nguyên tắc cốt lõi.  
- Trình bày lợi ích DevOps, các chỉ số hiệu suất chính:  
  - **DORA Metrics**  
  - **MTTR** (Mean Time to Recovery)  
  - Deployment frequency  

---

### 2. AWS DevOps Services – CI/CD Pipeline (9:00 – 10:30 AM)

Nội dung tập trung vào xây dựng pipeline CI/CD hoàn chỉnh sử dụng AWS-native services.

#### **Source Control**
- **AWS CodeCommit**  
- Chiến lược quản lý source:  
  - GitFlow  
  - Trunk-based development  

#### **Build & Test**
- **AWS CodeBuild**  
- Cấu hình buildspec.yml  
- Thiết kế pipeline testing  

#### **Deployment**
- **AWS CodeDeploy** hỗ trợ nhiều chiến lược:  
  - Blue/Green  
  - Canary  
  - Rolling updates  

#### **Orchestration**
- **AWS CodePipeline**  
- Tự động hóa CI/CD end-to-end  

#### **Live Demo**
- Walkthrough CI/CD pipeline hoàn chỉnh từ commit → build → test → deploy.

---

### 3. Break (10:30 – 10:45 AM)

---

### 4. Infrastructure as Code (IaC) (10:45 AM – 12:00 PM)

#### **AWS CloudFormation**
- Templates, stacks, change sets  
- Drift detection  

#### **AWS CDK (Cloud Development Kit)**
- Constructs  
- Reusable patterns  
- Hỗ trợ nhiều ngôn ngữ: TypeScript, Python, Java, C#  

#### **Live Demo**
- Deploy hạ tầng với CloudFormation & CDK  

#### **Thảo luận**
- So sánh ưu/nhược điểm của CloudFormation vs CDK  
- Tình huống chọn công cụ IaC phù hợp  

---

### Lunch Break (12:00 – 1:00 PM)

---

## Afternoon Session (1:00 PM – 5:00 PM)

### 5. Container Services on AWS (1:00 – 2:30 PM)

#### **Docker Fundamentals**
- Microservices  
- Containerization workflow  

#### **Amazon ECR**
- Image registry  
- Image scanning  
- Lifecycle policies  

#### **Amazon ECS & EKS**
- Deployment strategies  
- Auto scaling  
- Orchestration differences  
  - ECS: AWS-managed  
  - EKS: Kubernetes-native  

#### **AWS App Runner**
- Triển khai container đơn giản, fully managed  
- Tích hợp CI/CD nhanh chóng  

#### **Demo & Case Study**
- So sánh triển khai microservices trên ECS, EKS và App Runner.

---

### 6. Break (2:30 – 2:45 PM)

---

### 7. Monitoring & Observability (2:45 – 4:00 PM)

#### **Amazon CloudWatch**
- Metrics  
- Logs  
- Alarms  
- Dashboard  

#### **AWS X-Ray**
- Distributed tracing  
- Hiểu rõ luồng request & điểm nghẽn hiệu năng  

#### **Live Demo**
- Thiết lập full-stack observability: logs → metrics → traces  

#### **Best Practices**
- Alerting  
- Dashboards  
- On-call workflow  

---

### 8. DevOps Best Practices & Case Studies (4:00 – 4:45 PM)

- Deployment strategies  
  - Feature flags  
  - A/B testing  
- Automated testing → CI/CD integration  
- Incident management & postmortems  
- Case studies về chuyển đổi DevOps ở startup & enterprise  

---

### 9. Q&A & Wrap-up (4:45 – 5:00 PM)

- Định hướng nghề nghiệp DevOps  
- Lộ trình chứng chỉ AWS dành cho DevOps Engineer (DVA-C02, DOP-C02)

---

## Key Takeaways

### DevOps Fundamentals
- DevOps không chỉ là toolset mà là văn hóa hợp tác giữa Dev & Ops.  
- Các chỉ số như **DORA**, **MTTR**, **lead time** là tiêu chuẩn đánh giá hiệu quả DevOps.

### AWS DevOps Services
- AWS cung cấp bộ công cụ CI/CD mạnh mẽ và có khả năng tự động hóa toàn diện.  
- CodePipeline + CodeBuild + CodeDeploy = Full CI/CD workflow.

### Infrastructure as Code
- IaC là nền tảng bắt buộc cho DevOps hiện đại.  
- CloudFormation phù hợp enterprise; CDK linh hoạt và nhanh hơn cho development.

### Container Orchestration
- ECS đơn giản, dễ vận hành.  
- EKS mạnh cho Kubernetes ecosystem.  
- App Runner phù hợp startup, MVP, dịch vụ nhỏ.

### Observability
- CloudWatch & X-Ray cung cấp visibility end-to-end.  
- Observability giúp giảm MTTR và hỗ trợ on-call hiệu quả.

---

### Some event photos
*Add your event photos here*

---

> Đây là một workshop toàn diện giúp người tham dự hiểu rõ quy trình DevOps hiện đại trên AWS — từ CI/CD, IaC, container orchestration đến monitoring. Buổi học giúp củng cố tư duy DevOps, kỹ năng kỹ thuật và định hướng nghề nghiệp rõ ràng trong lĩnh vực Cloud & DevOps.

