---
title: "WEEK 1 WORKLOG"
date: "2025-11-10"
weight: 2
chapter: false
pre: " <b> 1.1 </b> "
---

# **WEEK 1 WORKLOG**

### **Week 1 Objectives**

* Understand and practice core AWS IAM concepts (Users, Groups, Roles, Policies).
* Learn to deploy and manage Amazon EC2 (Launch instances, Security Groups, Snapshots, AMIs).
* Implement a high-availability and auto-scaling architecture using Elastic Load Balancer (ELB) and Auto Scaling Group (ASG).
* Understand and apply IAM Roles as a secure method for EC2 to access other AWS services (like S3).

---

### **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Mon) | **Lab 02 – Introduction to AWS IAM**: Practice creating/managing IAM Users, Groups, Roles, Policies; perform Switch Role. | 08/09/2025 | 08/09/2025 | |
| 2 (Tue) | **Learn & Deploy Amazon EC2**: Launch EC2 instances (Windows & Linux); install Apache web server; practice creating Snapshots & AMIs. | 09/09/2025 | 09/09/2025 | |
| 3 (Wed) | **Security Group Lab**: Configure Security Groups (stateful firewall) to allow and block access (HTTP, SSH) to an EC2 instance. | 10/09/2025 | 10/09/2025 | |
| 4 (Thu) | **Deploy Auto-Scaling System**: Configure Launch Template, Auto Scaling Group (with CPU-based policy), and Application Load Balancer (ALB). | 11/09/2025 | 11/09/2025 | |
| 5 (Fri) | **Lab: Assign IAM Role to EC2 for S3 Access**: Create an S3 read-only IAM Role, assign it to EC2; use AWS CLI to test secure access. | 12/09/2025 | 12/09/2025 | |

---

### **Week 1 Achievements**

* Mastered basic concepts and practical operations of **AWS IAM**, understanding the differences between Users, Groups, Roles, and Policies.
* Successfully deployed and managed **Amazon EC2** virtual machines, including:
    * Launching instances from different AMIs (Linux, Windows).
    * Installing and configuring a basic Apache web server.
    * Backing up and cloning instances using Snapshots and AMIs.
* Understood and proficiently configured **Security Groups** to secure instances, applying the Principle of Least Privilege.
* Deployed a complete high-availability (HA) and auto-scaling architecture by combining:
    * **Launch Templates** for instance consistency.
    * **Application Load Balancer (ALB)** for traffic distribution.
    * **Auto Scaling Groups (ASG)** to automatically add/remove instances based on CPU load.
* Understood and applied the security best practice of using **IAM Roles** for EC2 to interact with S3, avoiding long-term access keys.
* Improved skills using the AWS Management Console and basic AWS CLI commands.