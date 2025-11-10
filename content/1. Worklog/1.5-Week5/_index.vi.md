---
title: "WEEK 5 WORKLOG"
date: "2025-11-10"
weight: 2
chapter: false
pre: " <b> 1.5 </b> "
---

# **WEEK 5 WORKLOG**

### **Week 5 Objectives**

* Tích hợp Amazon S3 vào ứng dụng web để lưu trữ và phục vụ tài nguyên tĩnh (hình ảnh).
* Tăng cường bảo mật cho ứng dụng web bằng cách triển khai AWS WAF (Web Application Firewall).
* Rà soát, tối ưu hóa (Security Group, EC2 Right-sizing) và viết tài liệu tổng kết cho dự án đã triển khai.
* Bắt đầu tìm hiểu về khái niệm Infrastructure as Code (IaC) và các thành phần cơ bản của AWS CloudFormation.

---

### **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Thứ Hai) | **Tích hợp S3 (Phần 1)**: Tạo S3 Bucket và cấu hình Bucket Policy cho phép truy cập công khai (public read). | 06/10/2025 | 06/10/2025 | |
| 2 (Thứ Ba) | **Triển khai AWS WAF**: Tạo một Web ACL, thêm các Rule bảo mật cơ bản (chặn IP) và gắn vào tài nguyên (ALB). | 07/10/2025 | 07/10/2025 | |
| 3 (Thứ Tư) | **Rà soát & Viết tài liệu**: Kiểm tra Security Group (chỉ mở port cần thiết), xem xét EC2 Right-sizing, viết tài liệu kiến trúc. | 08/10/2025 | 08/10/2025 | |
| 4 (Thứ Năm) | **Tích hợp S3 (Phần 2)**: Cập nhật mã nguồn ứng dụng (HTML/CSS) để sử dụng link ảnh từ S3 Bucket đã tạo. | 09/10/2025 | 09/10/2025 | |
| 5 (Thứ Sáu) | **Tìm hiểu IaC**: Đọc tài liệu tổng quan về IaC và xem video giới thiệu về các khái niệm cơ bản của AWS CloudFormation (Stacks, Templates). | 10/10/2025 | 10/10/2025 | |

---

### **Week 5 Achievements**

* Tích hợp thành công **Amazon S3** vào ứng dụng web để lưu trữ và phục vụ tài nguyên tĩnh (hình ảnh), giúp giảm tải cho web server và cải thiện hiệu suất.
* Cấu hình thành thạo **S3 Bucket Policy** để cho phép truy cập public read một cách an toàn.
* Triển khai một lớp bảo mật ứng dụng web bằng **AWS WAF**.
* Tạo thành công **Web ACL** và áp dụng các Rule cơ bản (như chặn IP) để bảo vệ tài nguyên (Application Load Balancer).
* Hoàn thành việc rà soát và tối ưu hóa tài nguyên cho dự án, bao gồm:
    * Siết chặt **Security Group** (chỉ mở các port cần thiết).
    * Xem xét **EC2 Right-sizing** để tối ưu chi phí và hiệu năng.
* Hoàn thành tài liệu mô tả kiến trúc và cách triển khai dự án.
* Bắt đầu tìm hiểu và nắm được các khái niệm cơ bản của **Infrastructure as Code (IaC)** và **AWS CloudFormation** (Stacks, Templates, Resources).