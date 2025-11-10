---
title: "WEEK 6 WORKLOG"
date: "2025-11-10"
weight: 1
chapter: false
pre: " <b> 1.6 </b> "
---

# **WEEK 6 WORKLOG**

### **Week 6 Objectives**

* Tìm hiểu sâu về **Infrastructure as Code (IaC)** bằng cách sử dụng **AWS CloudFormation**.
* Nắm vững cú pháp YAML và cấu trúc của một CloudFormation Template (bao gồm `Parameters`, `Resources`, `Outputs`).
* Viết template để tự động hóa việc tạo tài nguyên đơn lẻ (S3 Bucket) và một hạ tầng mạng phức tạp (VPC, Subnet, IGW, Route Table).
* Mở rộng template để tự động triển khai một máy chủ web hoàn chỉnh (EC2, Security Group) vào hạ tầng mạng đã tạo.
* Nắm vững quy trình quản lý vòng đời của stack (tạo, cập nhật, xóa) bằng AWS Console và AWS CLI.

---

### **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Thứ Hai) | **Tìm hiểu CloudFormation & YAML**: Nghiên cứu các section (Parameters, Resources, Outputs) và cú pháp YAML. Viết template đơn giản tạo S3 Bucket. | 13/10/2025 | 13/10/2025 | |
| 2 (Thứ Ba) | **Triển khai Stack & Parameters**: Deploy stack S3. Thêm `Parameters` (ví dụ: tùy chỉnh tên Bucket) vào template và học cách cập nhật stack. | 14/10/2025 | 14/10/2025 | |
| 3 (Thứ Tư) | **Viết template Mạng**: Viết template mới tạo hạ tầng mạng (VPC, Public Subnet, IGW, Route Table). Sử dụng `Outputs` để hiển thị IDs. | 15/10/2025 | 15/10/2025 | |
| 4 (Thứ Năm) | **Viết template EC2**: Mở rộng template mạng, thêm `Resources` cho Security Group (SSH, HTTP) và EC2 instance (chỉ định AMI, Type). | 16/10/2025 | 16/10/2025 | |
| 5 (Thứ Sáu) | **Triển khai & Dọn dẹp**: Deploy stack hoàn chỉnh (VPC + Subnet + EC2). Kiểm tra SSH/HTTP. Học cách xóa stack (`aws cloudformation delete-stack`). | 17/10/2025 | 17/10/2025 | |

---

### **Week 6 Achievements**

* Nắm vững cú pháp YAML và cấu trúc của một template **AWS CloudFormation** (bao gồm `Parameters`, `Resources`, `Outputs`).
* Viết thành công template CloudFormation để tự động hóa việc tạo các tài nguyên đơn lẻ (như **S3 Bucket**).
* Sử dụng thành thạo `Parameters` để tùy chỉnh tài nguyên khi triển khai (ví dụ: tên S3 Bucket, AMI ID, Instance Type), giúp tăng tính linh hoạt và tái sử dụng của template.
* Viết thành công một template phức tạp, liên kết nhiều tài nguyên để xây dựng hạ tầng mạng hoàn chỉnh, bao gồm:
    * **VPC** và **Public Subnet**.
    * **Internet Gateway (IGW)** và **Route Table** (cùng các association).
* Mở rộng template để tự động triển khai một máy chủ web, bao gồm:
    * **Security Group** (cho phép SSH port 22 và HTTP port 80).
    * **EC2 Instance** (sử dụng `!Ref` để liên kết với Subnet và Security Group đã tạo).
* Nắm vững quy trình quản lý stack: triển khai (`create-stack`), cập nhật (`update-stack`) và xóa (`delete-stack`) bằng cả AWS Console và **AWS CLI**.
* Khắc phục được các lỗi phổ biến khi làm việc với CloudFormation, như lỗi cú pháp YAML (thụt lề), tên S3 Bucket (duy nhất toàn cầu), AMI ID (theo region), và lỗi khi xóa stack (do tài nguyên phụ thuộc).