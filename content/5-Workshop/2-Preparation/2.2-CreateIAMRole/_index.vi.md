---
title : "Tạo IAM Role"
date : "2025-10-10"
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

Trong bước này, chúng ta sẽ tiến hành tạo IAM Role. Trong IAM Role này, chính sách **CloudWatchAgentServerPolicy** sẽ được gán, đây là chính sách cho phép sử dụng Amazon CloudWatch Agent trên các máy chủ.

1. Trên thanh tìm kiếm phía trên, nhập `IAM` và chọn dịch vụ **IAM** từ kết quả tìm kiếm.
![role](/images/2-Preparation/2.2-CreateIAMRole/01-SearchIAM.png)
2. Trong thanh điều hướng bên trái, nhấp vào **Roles** và sau đó nhấp vào **Create Role**.
![IAM Dashboard](/images/2-Preparation/2.2-CreateIAMRole/02-AccessIAMDashboard.png)
3. Trong trường **Select trusted entity**:
     - Trusted entity type: **AWS service**
     - Service or use case: **EC2**
     - Use case: **EC2**
![Trusted Entity](/images/2-Preparation/2.2-CreateIAMRole/03-SelectTrustedEntity.png)
4. Trong trường **Add permission**:
    - Nhập `CloudWatchAgentServerPolicy` vào thanh tìm kiếm
    - Chọn chính sách này
![Add permission](/images/2-Preparation/2.2-CreateIAMRole/04-AddPermission.png)
5. Trong trường **Name, review, and create**:
    - Role name: `RoleForEC2MonitoringUsingCloudWatchAgent`
    - Nhấp vào **Create role** để hoàn tất bước
    - Bạn nên kiểm tra kỹ các bước để đảm bảo không có lỗi nào xảy ra
![Check again](/images/2-Preparation/2.2-CreateIAMRole/05-ReviewAgain.png)
