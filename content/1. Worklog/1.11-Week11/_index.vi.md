---
title: "WEEK 11 WORKLOG"
date: "2025-11-10"
weight: 11
chapter: false
pre: " <b> 1.11 </b> "
---

# **WEEK 11 WORKLOG**

### **Week 11 Objectives**

* Tìm hiểu và thực hành các tính năng nâng cao của **Kubernetes** (K8s) bao gồm quản lý tài nguyên, auto-scaling, và bảo mật.
* Cấu hình thành công **Horizontal Pod Autoscaler (HPA)** để tự động co giãn Pod.
* Cấu hình thành công các chính sách bảo mật K8s như **Network Policies** và **RBAC**.
* Nghiên cứu về các hệ thống giám sát (Monitoring) và quản lý log (Logging) cho K8s (Prometheus, Grafana, ELK, Fluentd).
* Tìm hiểu và cấu hình tính năng nâng cao của **AWS Application Load Balancer (ALB)**, cụ thể là **Content-based Routing**.
* Nghiên cứu về hỗ trợ **HTTP/2** trên ALB.

---

### **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Thứ Hai) | **K8s Quản lý Tài nguyên & Scaling**: Học về Resource Quotas, Limit Ranges. Thực hành cấu hình **Horizontal Pod Autoscaler (HPA)**. | 17/11/2025 | 17/11/2025 | |
| 2 (Thứ Ba) | **K8s Security (Network)**: Thực hành cấu hình **Network Policies** để kiểm soát lưu lượng mạng giữa các Pod. Nghiên cứu các tool giám sát (Prometheus, Grafana, ELK). | 18/11/2025 | 18/11/2025 | |
| 3 (Thứ Tư) | **K8s Security (Access)**: Thực hành cấu hình **RBAC** (Roles, RoleBindings) để quản lý quyền truy cập. Nghiên cứu các tool quản lý log (Fluentd, ELK). | 19/11/2025 | 19/11/2025 | |
| 4 (Thứ Năm) | **Tìm hiểu ALB Content-based Routing**: Nghiên cứu và viết tài liệu chi tiết về cách ALB định tuyến lưu lượng dựa trên nội dung (path, header). | 20/11/2025 | 20/11/2025 | |
| 5 (Thứ Sáu) | **Cấu hình ALB & HTTP/2**: Thực hành cấu hình **Content-based Routing** (vd: `/api/*`). Gỡ lỗi. Nghiên cứu về hỗ trợ **HTTP/2** trên ALB. | 21/11/2025 | 21/11/2025 | |

---

### **Week 11 Achievements**

* Nắm vững các khái niệm quản lý tài nguyên trong Kubernetes như **Resource Quotas** và **Limit Ranges**.
* Cấu hình và triển khai thành công **Horizontal Pod Autoscaler (HPA)** bằng file YAML, cho phép hệ thống tự động co giãn (scale) số lượng Pod dựa trên tải CPU.
* Nắm vững và thực hành thành công các tính năng bảo mật quan trọng trong Kubernetes:
    * **Network Policies**: Viết và áp dụng file YAML để kiểm soát lưu lượng mạng (ingress) giữa các Pod.
    * **RBAC (Role-Based Access Control)**: Viết và áp dụng file YAML để tạo **Roles** và **RoleBindings**, quản lý quyền truy cập của người dùng (ví dụ: `pod-reader`).
* Nghiên cứu tổng quan về các hệ thống giám sát (**Prometheus**, **Grafana**) và quản lý log (**ELK Stack**, **Fluentd**) phổ biến trong hệ sinh thái K8s.
* Nắm vững và viết tài liệu chi tiết về tính năng **Content-based Routing** của AWS Application Load Balancer (ALB).
* Cấu hình thành công các quy tắc (rules) trên ALB Listener để định tuyến lưu lượng truy cập đến các Target Group khác nhau dựa trên đường dẫn URL (ví dụ: `/api/*`).
* Khắc phục được các sự cố cấu hình khi HPA không hoạt động hoặc Network Policy không được áp dụng đúng.
* Tìm hiểu về lợi ích và cách kích hoạt hỗ trợ **HTTP/2** trên ALB (thông qua listener HTTPS).
