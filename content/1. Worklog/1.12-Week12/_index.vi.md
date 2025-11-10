---
title: "WEEK 12 WORKLOG"
date: "2025-11-10"
weight: 2
chapter: false
pre: " <b> 1.12 </b> "
---

# **WEEK 12 WORKLOG**

### **Week 12 Objectives**

* Hoàn thiện và tối ưu hóa cấu hình **AWS Application Load Balancer (ALB)**.
* Tìm hiểu và cấu hình thành công các tính năng nâng cao của ALB bao gồm **HTTP/2**, **WebSocket**, và **Sticky Sessions**.
* Thực hiện kiểm tra hiệu suất (Performance Testing) cho ALB để đánh giá khả năng chịu tải.
* Hoàn thành workshop và chuẩn bị báo cáo tổng kết kỳ thực tập.

---

### **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Thứ Hai) | **Tìm hiểu & Cấu hình HTTP/2**: Nghiên cứu và cấu hình ALB Listener (HTTPS) để hỗ trợ **HTTP/2**. Nghiên cứu sơ bộ về **WebSocket**. | 24/11/2025 | 24/11/2025 | |
| 2 (Thứ Ba) | **Cấu hình WebSocket**: Cấu hình ALB Listener để hỗ trợ **WebSocket** và kiểm tra kết nối. Tối ưu hóa cài đặt timeout. | 25/11/2025 | 25/11/2025 | |
| 3 (Thứ Tư) | **Cấu hình Sticky Sessions (Phần 1)**: Cấu hình **Sticky Sessions** (Target Group Attributes) để duy trì phiên làm việc. Thực hiện **Health Checks**. | 26/11/2025 | 26/11/2025 | |
| 4 (Thứ Năm) | **Cấu hình Sticky Sessions (Phần 2)**: (Nội dung lặp lại) Kiểm tra và xác nhận tính năng Sticky Sessions hoạt động. | 27/11/2025 | 27/11/2025 | |
| 5 (Thứ Sáu) | **Kiểm thử Hiệu suất (Performance Testing)**: Sử dụng công cụ (JMeter/Gatling) để kiểm thử tải ALB. Phân tích kết quả và hoàn thành báo cáo. | 28/11/2025 | 28/11/2025 | |

---

### **Week 12 Achievements**

* Cấu hình thành công **Application Load Balancer (ALB)** để hỗ trợ giao thức **HTTP/2** (qua listener HTTPS), hiểu rõ lợi ích về hiệu suất của nó.
* Cấu hình thành công ALB để hỗ trợ kết nối **WebSocket**, cho phép giao tiếp hai chiều (real-time) và khắc phục được sự cố về `idle timeout`.
* Cấu hình và kiểm tra thành công tính năng **Sticky Sessions** (Application-based cookie) trên Target Group, đảm bảo các yêu cầu từ một client được chuyển hướng đến cùng một instance.
* Thực hiện thành công các bài kiểm tra **Health Checks** để đảm bảo các instance trong Target Group ở trạng thái khỏe mạnh.
* Thực hiện **Kiểm thử hiệu suất (Performance Testing)** cho ALB bằng cách sử dụng các công cụ tạo tải (như JMeter), phân tích các chỉ số (thời gian phản hồi, tỷ lệ lỗi) và xác định các điểm cần tối ưu.
* Hoàn thành workshop cuối cùng và chuẩn bị báo cáo tổng kết cho toàn bộ 12 tuần thực tập.