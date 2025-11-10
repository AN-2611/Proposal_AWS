---
title: "WEEK 2 WORKLOG"
date: "2025-11-10"
weight: 1
chapter: false
pre: " <b> 1.2 </b> "
---

# **WEEK 2 WORKLOG**

### **Week 2 Objectives**

* Hiểu và thực hành về dịch vụ giám sát **AWS CloudWatch** (Metrics, Alarms, Logs, Dashboards, Agent).
* Tìm hiểu và thực hành về quản lý đa tài khoản với **AWS Organizations** (OUs, creating accounts, inviting accounts, member vs. management roles).
* Tìm hiểu và triển khai **AWS Storage Gateway**, tích hợp với S3 và EC2.

---

### **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Thứ Hai) | **Lab 08 – AWS CloudWatch (Phần 1)**: Cấu hình EC2; tạo CloudWatch Alarm (CPU Utilization) và CloudWatch Dashboard. | 15/09/2025 | 15/09/2025 | |
| 2 (Thứ Ba) | **Lab 08 – AWS CloudWatch (Phần 2)**: Cài đặt và cấu hình CloudWatch Agent trên EC2 để thu thập và đẩy logs ứng dụng lên CloudWatch Logs. | 16/09/2025 | 16/09/2025 | |
| 3 (Thứ Tư) | **Tìm hiểu AWS Organizations (Phần 1)**: Tạo tài khoản thành viên (member account) mới và cấu trúc các tài khoản bằng Organizational Units (OUs). | 17/09/2025 | 17/09/2025 | |
| 4 (Thứ Năm) | **Triển khai AWS Storage Gateway**: Chuẩn bị S3 Bucket; khởi tạo EC2 instance và cài đặt Storage Gateway. | 18/09/2025 | 18/09/2025 | |
| 5 (Thứ Sáu) | **Tìm hiểu AWS Organizations (Phần 2)**: Mời một tài khoản AWS có sẵn tham gia vào Organization; thực hành truy cập (switch role) giữa tài khoản quản lý và tài khoản thành viên. | 19/09/2025 | 19/09/2025 | |

---

### **Week 2 Achievements**

* Nắm vững cách theo dõi, tạo cảnh báo (Alarms) và trực quan hóa (Dashboards) cho tài nguyên EC2 bằng **CloudWatch Metrics**.
* Cài đặt và cấu hình thành công **CloudWatch Agent** để thu thập và đẩy logs từ EC2 lên **CloudWatch Logs** một cách tập trung.
* Hiểu rõ sự khác biệt và tầm quan trọng của Metrics (giám sát) và Logs (ghi log) trong vận hành hệ thống.
* Nắm vững khái niệm và lợi ích của **AWS Organizations** trong việc quản lý đa tài khoản.
* Thực hành thành công việc tạo mới tài khoản (member account) và mời tài khoản có sẵn vào Organization.
* Hiểu và cấu trúc được các tài khoản bằng **Organizational Units (OUs)**.
* Thực hành thành công việc truy cập chéo (switch role) giữa tài khoản quản lý (management) và tài khoản thành viên (member).
* Triển khai và cấu hình cơ bản thành công **AWS Storage Gateway** trên một EC2 instance.
* Khắc phục được các sự cố kết nối liên quan đến **IAM Roles** và **Security Groups** khi EC2 tương tác với các dịch vụ khác (S3, CloudWatch, Storage Gateway), củng cố kiến thức Tuần 1.