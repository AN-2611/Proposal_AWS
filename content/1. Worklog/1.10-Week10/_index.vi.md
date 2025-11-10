---
title: "WEEK 10 WORKLOG"
date: "2025-11-10"
weight: 1
chapter: false
pre: " <b> 1.10 </b> "
---

# **WEEK 10 WORKLOG**

### **Week 10 Objectives**

* Tìm hiểu về hệ thống điều phối container (container orchestration) với **Kubernetes**.
* Nắm vững các khái niệm cốt lõi của Kubernetes (Cluster, Node, Pod) và cách viết file cấu hình YAML.
* Thực hành triển khai ứng dụng (Node.js) lên cluster Kubernetes (sử dụng Minikube).
* Tìm hiểu về các công cụ giám sát (monitoring) cho container (Prometheus, Grafana, cAdvisor).
* Tìm hiểu về giải pháp sao lưu và phục hồi (backup & disaster recovery) cho Kubernetes bằng **Velero**.
* Ôn lại tài liệu và chuẩn bị cho buổi báo cáo tổng kết về CI/CD.

---

### **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Thứ Hai) | **Tìm hiểu Kubernetes**: Học về kiến trúc (Pod, Node, Cluster). Viết file `deployment.yaml` và deploy ứng dụng (`kubectl apply`) lên Minikube. | 10/11/2025 | 10/11/2025 | |
| 2 (Thứ Ba) | **Tìm hiểu Monitoring & Báo cáo CI/CD**: (Nội dung lặp lại) Ôn tập tài liệu CI/CD. Tìm hiểu về các công cụ giám sát (Prometheus, Grafana). | 11/11/2025 | 11/11/2025 | |
| 3 (Thứ Tư) | **Tìm hiểu Monitoring & Báo cáo CI/CD**: (Nội dung lặp lại) Ôn tập tài liệu CI/CD. Tìm hiểu về các công cụ giám sát (Prometheus, Grafana). | 12/11/2025 | 12/11/2025 | |
| 4 (Thứ Năm) | **Tìm hiểu Monitoring & Báo cáo CI/CD**: (Nội dung lặp lại) Ôn tập tài liệu CI/CD. Tìm hiểu về các công cụ giám sát (Prometheus, Grafana). | 13/11/2025 | 13/11/2025 | |
| 5 (Thứ Sáu) | **Tìm hiểu Backup (Velero)**: Cài đặt và cấu hình **Velero** (dùng Helm). Thực hành sao lưu (`velero backup create`) và phục hồi (`velero restore create`) tài nguyên. | 14/11/2025 | 14/11/2025 | |

---

### **Week 10 Achievements**

* Nắm vững các khái niệm cơ bản của **Kubernetes** (K8s) bao gồm **Cluster**, **Node**, và **Pod**.
* Viết thành công file cấu hình `deployment.yaml` và triển khai một ứng dụng Node.js lên cluster Kubernetes (Minikube) bằng `kubectl apply`.
* Tìm hiểu và khắc phục được sự cố khi thiết lập môi trường Kubernetes local (sử dụng Minikube để giải quyết vấn đề tài nguyên).
* Tìm hiểu về các công cụ giám sát (monitoring) và trực quan hóa (visualization) phổ biến trong hệ sinh thái container, bao gồm **Prometheus**, **Grafana**, và **cAdvisor**.
* Nắm vững khái niệm về sao lưu và phục hồi thảm họa (Disaster Recovery) trong Kubernetes.
* Cài đặt và sử dụng thành công **Velero** để thực hiện sao lưu (`backup`) và phục hồi (`restore`) các tài nguyên trong cluster.
* Hoàn thành việc xem lại và chuẩn bị tài liệu cho buổi báo cáo tổng kết về chủ đề CI/CD.