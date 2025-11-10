---
title: "WEEK 9 WORKLOG"
date: "2025-11-10"
weight: 2
chapter: false
pre: " <b> 1.9 </b> "
---

# **WEEK 9 WORKLOG**

### **Week 9 Objectives**

* Tìm hiểu về kiến trúc Serverless (phi máy chủ) và thực hành với **AWS Lambda**.
* Tìm hiểu về các công cụ CI/CD (Continuous Integration) và thực hành cài đặt, cấu hình **Jenkins** để kiểm tra tự động.
* Tìm hiểu về công nghệ container hóa (containerization) với **Docker**.
* Viết **Dockerfile** cho ứng dụng (Node.js) và thực hành build/run container.
* Tìm hiểu và thực hành dịch vụ triển khai tự động **AWS CodeDeploy**.
* Tìm hiểu về các công cụ giám sát (monitoring) cho container (Prometheus, Grafana).

---

### **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Thứ Hai) | **Tìm hiểu AWS Lambda**: Nghiên cứu về Serverless, tạo một hàm Lambda đơn giản (kích hoạt từ S3) và đánh giá cách tích hợp vào CI/CD. | 03/11/2025 | 03/11/2025 | |
| 2 (Thứ Ba) | **Tìm hiểu CI & Jenkins**: Nghiên cứu các công cụ CI (Jenkins, Travis CI), thực hành cài đặt và cấu hình **Jenkins** (tạo pipeline) để kiểm tra tự động. | 04/11/2025 | 04/11/2025 | |
| 3 (Thứ Tư) | **Tìm hiểu Docker**: Nghiên cứu về container. Thực hành viết **Dockerfile** cho ứng dụng Node.js, build image (`docker build`) và chạy container (`docker run`). | 05/11/2025 | 05/11/2025 | |
| 4 (Thứ Năm) | **Tìm hiểu AWS CodeDeploy**: Nghiên cứu dịch vụ CodeDeploy. Thực hành triển khai ứng dụng mẫu (từ CodeCommit) lên EC2 và gỡ lỗi tập lệnh (script). | 06/11/2025 | 06/11/2025 | |
| 5 (Thứ Sáu) | **Tìm hiểu Monitoring & Báo cáo**: Xem lại tài liệu CI/CD. Tìm hiểu về các công cụ giám sát container (Prometheus, Grafana, cAdvisor). | 07/11/2025 | 07/11/2025 | |

---

### **Week 9 Achievements**

* Nắm vững khái niệm về **Serverless** và thực hành tạo thành công một hàm **AWS Lambda** cơ bản, xử lý sự kiện từ S3.
* Khắc phục được sự cố về **IAM Role** khi cấu hình quyền cho Lambda truy cập S3.
* Nắm vững khái niệm về Tích hợp liên tục (CI) và vai trò của các công cụ như **Jenkins**.
* Cài đặt và cấu hình thành công một máy chủ **Jenkins** cơ bản, tạo một pipeline đơn giản để kiểm tra tự động.
* Nắm vững khái niệm cốt lõi về **Docker** và containerization.
* Viết thành công một **Dockerfile** cho ứng dụng Node.js, build image và chạy ứng dụng trong container một cách nhất quán.
* Nắm vững và thực hành thành công dịch vụ **AWS CodeDeploy**, tự động hóa việc triển khai ứng dụng từ CodeCommit lên EC2.
* Khắc phục được lỗi tập lệnh (deployment script) trong quá trình triển khai với CodeDeploy.
* Tìm hiểu tổng quan về các công cụ giám sát container phổ biến như **Prometheus** và **Grafana**.