---
title : "Tạo IAM Policy"
date : "2025-10-10"
weight : 3
chapter : false
pre : " <b> 2.3 </b> "
---

Trước khi gán các chính sách vào role, chúng ta sẽ tạo một chính sách tùy chỉnh của riêng mình.

1. Trên trang **Policies**, nhấp chuột phải vào nút **Create policy** và mở nó trong một tab trình duyệt mới.
![Find Policies](/images/2-Preparation/2.3-CreateIAMPolicy/01-PoliciesDashboard.png)

2. Trong trang **Specify permissions**:
   - **Service:** S3
   - **Action allowed:** `GetObject` và `ListBucket`
   - **Resources**: `alb-access-logs-137`
![Find Policies](/images/2-Preparation/2.3-CreateIAMPolicy/02-ConfigPermiss.png)

3. Chọn **Add more permission** để thêm quyền SNS với hành động `Publish` được cho phép.
![SNS policy](/images/2-Preparation/2.3-CreateIAMPolicy/06-SNSPolicy.png)

4. Trong phần **Review and create**:
   - **Policy name:** `S3-SNS-Policy`
   - **Description:** `Grants read access to a specific S3 bucket and publish access to an SNS topic`
![Find Policies](/images/2-Preparation/2.3-CreateIAMPolicy/03-Review.png)

5. Chúng ta cần gán chính sách đã tạo vào role **CloudWatchAgentServerPolicy**. Truy cập vào role **CloudWatchAgentServerPolicy**, chọn **Add permission**.
![Find Policies](/images/2-Preparation/2.3-CreateIAMPolicy/04-AddPermiss.png)

6. Nhập `S3-SNS-Policy` vào thanh tìm kiếm. Chọn **Add permission**.
![Find Policies](/images/2-Preparation/2.3-CreateIAMPolicy/05-AddPermissPage.png)
