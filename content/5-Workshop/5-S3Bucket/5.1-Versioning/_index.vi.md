
---
title : "Tạo S3 bucket và bật tính năng Versioning"
date : "2025-10-10"
weight : 2
chapter : false
pre : " <b> 5.1 </b> "
---

Chúng ta sẽ tạo S3 bucket để chứa nhật ký (logs) từ EC2 và ALB.

1. Trong AWS Management Console, điều hướng đến dịch vụ S3.
![Tìm kiếm](/images/5-S3Bucket/5.1-Versioning/01-Find.png)

2. Nhấp vào nút **Create bucket**.

3. Trong trang **Create bucket**:
   - **Bucket name:** `alb-access-logs-173`
   - **Bucket Versioning**: Bật (Enable)
   - Giữ nguyên các tùy chọn khác theo mặc định.
> 💡Thực tiễn tốt nhất: Tính năng Versioning giúp bảo vệ nhật ký của bạn khỏi bị ghi đè hoặc xóa nhầm, điều này rất quan trọng để duy trì một bản ghi kiểm toán đầy đủ.

![Cấu hình tạo Bucket](/images/5-S3Bucket/5.1-Versioning/02-ConfigCreateBucket.png)

4. Chuyển đến trang **Permissions**, cuộn xuống phần **Bucket policy**, chọn **Edit**.
![Trang quyền hạn](/images/5-S3Bucket/5.1-Versioning/03-PermissionPage.png)

5. Dán đoạn mã sau. Bạn phải thay thế ba chỗ giữ chỗ:

{{% notice warning %}}
Chúng ta đã tạo ALB ở khu vực **N. Virginia**, yêu cầu ID của tài khoản Elastic Load Balancing cho khu vực đó. Bạn nên truy cập vào [Enable access logs for your Application Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/enable-access-logging.html) để tìm ID phù hợp.
{{% /notice %}}

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": "logdelivery.elasticloadbalancing.amazonaws.com"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::[BUCKET_NAME]/AWSLogs/[YOUR_AWS_ACCOUNT_ID]/"
        }
    ]
}
```
