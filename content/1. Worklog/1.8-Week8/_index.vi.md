---
title: "WEEK 8 WORKLOG"
date: "2025-11-10"
weight: 2
chapter: false
pre: " <b> 1.8 </b> "
---

# **WEEK 8 WORKLOG**

### **Week 8 Objectives**

* Thực hành và hoàn thiện kỹ năng sử dụng **Terraform** (IaC).
* Nắm vững cách sử dụng **biến (variables)** và file `.tfvars` trong Terraform để quản lý cấu hình một cách linh hoạt.
* Tìm hiểu và xây dựng một quy trình **CI/CD (Continuous Integration/Continuous Delivery)** hoàn chỉnh trên AWS.
* Cấu hình **AWS CodePipeline** để tự động hóa các bước build, test, và deploy.
* Tìm hiểu và thực hành triển khai ứng dụng tự động lên EC2 bằng **AWS CodeDeploy**.
* Tích hợp các bước kiểm tra tự động (automated testing) vào pipeline.

---

### **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Thứ Hai) | **Terraform Apply & Variables**: Chạy `terraform apply` để tạo S3 bucket. Refactor code, thêm `variable` và file `.tfvars` để quản lý tên bucket. | 27/10/2025 | 27/10/2025 | |
| 2 (Thứ Ba) | **Terraform Practice**: (Tiếp tục thực hành và củng cố kiến thức về Terraform variables và `.tfvars` từ ngày hôm trước). | 28/10/2025 | 28/10/2025 | |
| 3 (Thứ Tư) | **Tìm hiểu CI/CD & CodePipeline**: Cấu hình pipeline CI/CD cơ bản (từ CodeCommit đến S3) bằng **AWS CodePipeline**. Bắt đầu tìm hiểu về **AWS CodeDeploy**. | 29/10/2025 | 29/10/2025 | |
| 4 (Thứ Năm) | **Tích hợp Testing vào Pipeline**: Tìm hiểu và cấu hình các bước kiểm tra tự động (automated testing, vd: unit tests) vào CodePipeline (sử dụng AWS CodeBuild). | 30/10/2025 | 30/10/2025 | |
| 5 (Thứ Sáu) | **Thực hành CodeDeploy**: Thực hành triển khai một ứng dụng mẫu (từ CodeCommit) lên EC2 instance bằng **AWS CodeDeploy**, xử lý lỗi tập lệnh (script). | 31/10/2025 | 31/10/2025 | |

---

### **Week 8 Achievements**

* Thực thi thành công `terraform apply` để tự động tạo tài nguyên (S3 Bucket) trên AWS.
* Nắm vững cách tham số hóa cấu hình Terraform bằng cách sử dụng **biến (variables)** (khai báo trong `.tf`) và quản lý giá trị biến tập trung qua file **`.tfvars`**.
* Hiểu rõ khái niệm và lợi ích của quy trình CI/CD (Continuous Integration/Continuous Delivery).
* Xây dựng thành công một pipeline CI/CD cơ bản bằng **AWS CodePipeline**, tự động hóa quy trình từ source (CodeCommit) đến deploy.
* Tích hợp thành công bước kiểm tra tự động (automated testing) vào pipeline (sử dụng **AWS CodeBuild**).
* Nắm vững và thực hành thành công cách triển khai ứng dụng tự động lên EC2 bằng **AWS CodeDeploy**, bao gồm cả việc gỡ lỗi các tập lệnh (deployment scripts).
* Kết thúc 8 tuần thực tập với kiến thức vững chắc về cả hạ tầng AWS (VPC, EC2, S3, IAM, WAF, v.v.), Infrastructure as Code (CloudFormation, Terraform), và quy trình DevOps (CI/CD với CodePipeline).