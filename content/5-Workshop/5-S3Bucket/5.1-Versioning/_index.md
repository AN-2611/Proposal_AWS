---
title : "Create S3 bucket and enable Versioning feature "
date : "2025-10-10"
weight : 2
chapter : false
pre : " <b> 5.1 </b> "
---
We will create S3 bucket to contains logs from EC2 and ALB also
1. In the AWS Management Console, navigate to the S3 service.
![Find](/images/5-S3Bucket/5.1-Versioning/01-Find.png)
2. Click the **Create bucket** button.
3. In the **Create bucket** page:
   - **Bucket name:** `alb-access-logs-173`
   - **Bucket Versioning**: Enable
   - Leave the other options as their defaults 
> 💡Best Practice: Versioning protects your logs from being accidentally overwritten or deleted, which is crucial for maintaining a complete audit trail.

![Find](/images/5-S3Bucket/5.1-Versioning/02-ConfigCreateBucket.png)
4. Go the **Permissions** page, scroll down to **Bucket policy**, choose **Edit**
![Permission Page](/images/5-S3Bucket/5.1-Versioning/03-PermissionPage.png)
5. Paste the following code. You must replace the three placeholders:
{{% notice warning %}}
We created ALB in **N. Virginia** region, which require ID of the Elastic Load Balancing account for the Region. You should access to [Enable access logs for your Application Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/enable-access-logging.html) to find an ID properly
{{% /notice %}}

```
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

