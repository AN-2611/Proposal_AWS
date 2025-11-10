---
title: "WEEK 6 WORKLOG"
date: "2025-11-10"
weight: 2
chapter: false
pre: " <b> 1.6 </b> "
---

# **WEEK 6 WORKLOG**

### **Week 6 Objectives**

* Take a deep dive into **Infrastructure as Code (IaC)** using **AWS CloudFormation**.
* Master YAML syntax and the structure of a CloudFormation Template (including `Parameters`, `Resources`, `Outputs`).
* Write templates to automate the creation of single resources (S3 Bucket) and a complex network (VPC, Subnet, IGW).
* Extend the template to automate the deployment of a full web server (EC2, Security Group).
* Master the stack lifecycle management process (create, update, delete) using the AWS Console and CLI.

---

### **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Mon) | **Learn CloudFormation & YAML**: Study sections (Parameters, Resources) and YAML syntax. Write a simple S3 Bucket template. | 13/10/2025 | 13/10/2025 | |
| 2 (Tue) | **Deploy Stack & Parameters**: Deploy the S3 stack. Add `Parameters` (e.g., custom bucket name) to the template and learn to update the stack. | 14/10/2025 | 14/10/2025 | |
| 3 (Wed) | **Write Network Template**: Write a new template for network infrastructure (VPC, Public Subnet, IGW, Route Table). Use `Outputs`. | 15/10/2025 | 15/10/2025 | |
| 4 (Thu) | **Write EC2 Template**: Extend the network template, adding `Resources` for a Security Group (SSH, HTTP) and an EC2 instance (specifying AMI). | 16/10/2025 | 16/10/2025 | |
| 5 (Fri) | **Deploy & Cleanup**: Deploy the complete stack (VPC + EC2). Test SSH/HTTP access. Learn to delete the stack (`aws cloudformation delete-stack`). | 17/10/2025 | 17/10/2025 | |

---

### **Week 6 Achievements**

* Mastered YAML syntax and the structure of an **AWS CloudFormation** template (including `Parameters`, `Resources`, `Outputs`).
* Successfully wrote a template to automate the creation of an **S3 Bucket**.
* Proficiently used `Parameters` to customize resources at deployment (e.g., bucket name, AMI ID), increasing template flexibility.
* Successfully wrote a complex, multi-resource template to build a complete network infrastructure, including:
    * **VPC** and **Public Subnet**.
    * **Internet Gateway (IGW)** and **Route Table** (with associations).
* Extended the template to automatically deploy a complete web server, including:
    * **Security Group** (allowing SSH port 22 and HTTP port 80).
    * **EC2 Instance** (using `!Ref` to link to the created Subnet and Security Group).
* Mastered the stack management lifecycle: deploy (`create-stack`), update (`update-stack`), and delete (`delete-stack`) via both AWS Console and **AWS CLI**.
* Troubleshot common CloudFormation errors: YAML indentation, S3 global unique names, region-specific AMIs, and resource dependencies on deletion.