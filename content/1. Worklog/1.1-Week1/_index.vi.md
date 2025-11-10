---
title: "WEEK 1 WORKLOG"
date: "2025-11-10"
weight: 1
chapter: false
pre: " <b> 1.1 </b> "
---

# **WEEK 1 WORKLOG**

### **Week 1 Objectives**

* Hiểu và thực hành về các khái niệm cốt lõi của AWS IAM (Users, Groups, Roles, Policies).
* Tìm hiểu, triển khai và quản trị dịch vụ Amazon EC2 (Launch instances, Security Groups, Snapshots, AMIs).
* Triển khai kiến trúc ứng dụng có tính sẵn sàng cao (High Availability) và tự động co giãn (Scalability) bằng cách sử dụng Elastic Load Balancer (ELB) và Auto Scaling Group (ASG).
* Hiểu và áp dụng IAM Role như một phương pháp bảo mật để cấp quyền cho EC2 truy cập các dịch vụ AWS khác (như S3).

---

### **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Thứ Hai) | **Lab 02 – Introduction to AWS IAM**: Thực hành tạo và quản lý IAM Users, Groups, Roles, và Policies; thực hiện Switch Role. | 08/09/2025 | 08/09/2025 | |
| 2 (Thứ Ba) | **Tìm hiểu và triển khai Amazon EC2**: Khởi chạy EC2 instance (Windows & Linux); cài đặt Apache web server; thực hành tạo Snapshot và AMI. | 09/09/2025 | 09/09/2025 | |
| 3 (Thứ Tư) | **Thực hành Lab về Security Group**: Cấu hình Security Group (stateful firewall) để cho phép và chặn truy cập (HTTP, SSH) vào EC2 instance. | 10/09/2025 | 10/09/2025 | |
| 4 (Thứ Năm) | **Triển khai hệ thống tự động co giãn**: Cấu hình Launch Template, Auto Scaling Group (với chính sách co giãn theo CPU), và Application Load Balancer (ALB) để phân phối tải. | 11/09/2025 | 11/09/2025 | |
| 5 (Thứ Sáu) | **Lab: Gán IAM Role cho EC2 truy cập S3**: Tạo IAM Role với quyền S3 read-only và gán cho EC2; sử dụng AWS CLI để kiểm tra truy cập an toàn. | 12/09/2025 | 12/09/2025 | |

---

### **Week 1 Achievements**

* Nắm vững các khái niệm cơ bản và thao tác thực tế với **AWS IAM**, hiểu rõ sự khác biệt giữa User, Group, Role và Policy.
* Triển khai và quản trị thành công máy ảo **Amazon EC2**, bao gồm:
    * Khởi chạy instance từ các AMI khác nhau (Linux, Windows).
    * Cài đặt và cấu hình một web server (Apache) cơ bản.
    * Thực hiện sao lưu và nhân bản instance bằng Snapshots và AMIs.
* Hiểu rõ và cấu hình thành thạo **Security Group** để bảo mật instance, áp dụng nguyên tắc đặc quyền tối thiểu (Principle of Least Privilege).
* Triển khai hoàn chỉnh một kiến trúc ứng dụng có tính sẵn sàng cao (HA) và tự động co giãn bằng cách kết hợp:
    * **Launch Templates** để đảm bảo tính nhất quán.
    * **Application Load Balancer (ALB)** để phân phối tải.
    * **Auto Scaling Groups (ASG)** để tự động thêm/bớt instance dựa trên tải CPU.
* Hiểu và áp dụng được phương pháp bảo mật tốt nhất (best practice) khi cho phép EC2 tương tác với các dịch vụ khác (S3) thông qua **IAM Roles**, thay vì lưu trữ access key dài hạn.
* Cải thiện kỹ năng sử dụng AWS Management Console và các lệnh cơ bản của AWS CLI.