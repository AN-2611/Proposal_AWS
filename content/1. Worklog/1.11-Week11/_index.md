---
title: "WEEK 11 WORKLOG"
date: "2025-11-10"
weight: 2
chapter: false
pre: " <b> 1.11 </b> "
---

# **WEEK 11 WORKLOG**

### **Week 11 Objectives**

* Learn and practice advanced **Kubernetes (K8s)** features, including resource management, auto-scaling, and security.
* Successfully configure the **Horizontal Pod Autoscaler (HPA)**.
* Successfully configure K8s security policies like **Network Policies** and **RBAC**.
* Research K8s monitoring and logging stacks (Prometheus, Grafana, ELK, Fluentd).
* Learn and configure advanced **AWS Application Load Balancer (ALB)** features, specifically **Content-based Routing**.
* Research **HTTP/2** support on the ALB.

---

### **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Mon) | **K8s Resource Mgmt & Scaling**: Learn Resource Quotas, Limit Ranges. Practice configuring **Horizontal Pod Autoscaler (HPA)**. | 17/11/2025 | 17/11/2025 | |
| 2 (Tue) | **K8s Security (Network)**: Practice configuring **Network Policies** to control pod traffic. Research monitoring tools (Prometheus, ELK). | 18/11/2025 | 18/11/2025 | |
| 3 (Wed) | **K8s Security (Access)**: Practice configuring **RBAC** (Roles, RoleBindings). Research logging tools (Fluentd, ELK). | 19/11/2025 | 19/11/2025 | |
| 4 (Thu) | **Learn ALB Content-based Routing**: Research and write detailed documentation on how ALB routes traffic based on content (path, header). | 20/11/2025 | 20/11/2025 | |
| 5 (Fri) | **Configure ALB & HTTP/2**: Practice configuring **Content-based Routing** (e.g., `/api/*`). Debug. Research **HTTP/2** support on ALB. | 21/11/2025 | 21/11/2025 | |

---

### **Week 11 Achievements**

* Mastered Kubernetes resource management concepts like **Resource Quotas** and **Limit Ranges**.
* Successfully configured and deployed a **Horizontal Pod Autoscaler (HPA)** using YAML to automatically scale Pods based on CPU load.
* Mastered and implemented critical Kubernetes security features:
    * **Network Policies**: Wrote and applied YAML to control network traffic (ingress) between Pods.
    * **RBAC (Role-Based Access Control)**: Wrote and applied YAML to create **Roles** and **RoleBindings** to manage user permissions.
* Researched an overview of popular monitoring (**Prometheus**, **Grafana**) and logging (**ELK Stack**, **Fluentd**) stacks for K8s.
* Mastered and wrote detailed documentation for the **Content-based Routing** feature of AWS Application Load Balancer (ALB).
* Successfully configured ALB Listener rules to route traffic to different Target Groups based on URL paths (e.g., `/api/*`).
* Troubleshot and resolved configuration issues (e.g., HPA not scaling, Network Policy not applying).
* Learned the benefits of and how to enable **HTTP/2** support on an ALB (via an HTTPS listener).