---
title : "Initialize S3 Bucket"
date :  "2025-10-10" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---
![S3 Bucket](/images/5-S3Bucket/s3_image.png)
### Introduce
Amazon S3 (Simple Storage Service) is a highly durable and scalable object storage service. Think of it as a nearly infinite hard drive in the cloud, perfect for storing data like application assets, backups, and, most importantly for this step, logs.

We're creating this specific S3 bucket to receive and store the access logs from our Application Load Balancer (ALB). These logs are incredibly valuable as they record detailed information about every single request made to your load balancer. This data is essential for analyzing traffic patterns, troubleshooting application errors, and conducting security audits.

We'll enable two key features:
   - **Versioning**: This protects your logs by keeping a complete history of all objects, preventing accidental overwrites or deletions.
   - **Bucket Policy:** This is a required security step that explicitly grants the ALB service permission to write log files into your bucket.

### Cost
- [S3 Pricing](https://aws.amazon.com/s3/pricing/)
### References
- [S3 documentation](https://docs.aws.amazon.com/s3/)
- [S3 Versioning](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Versioning.html)
### Content
1. [Create S3 bucket and enable Versioning feature](5-S3Bucket/5.1-Versioning)