+++
title = "Create SNS topic"
date = 2022
weight = 10
chapter = false
pre = "<b>10. </b>"
+++
### Introduce
![iconASG](/images/10-SNS/icon.png)

**Amazon SNS (Simple Notification Service)** is a flexible and fully managed messaging service for sending notifications. It operates on a publish/subscribe (pub/sub) model.

Think of an SNS Topic as a central communication channel or a notification hub. Other AWS services, like CloudWatch, can "publish" a message (an alert) to this topic. Then, SNS instantly delivers that message to all the "subscribers" of the topic.

Subscribers can be anything from email addresses and mobile numbers (SMS) to other AWS services like Lambda functions or SQS queues. In this step, we'll create a topic named **alb-alerts** and subscribe an email address to it, so you can receive important notifications directly in your inbox. 

### Cost
- [Amazon SNS pricing](https://aws.amazon.com/sns/pricing/)

### Documentation
- [Amazon SNS](https://docs.aws.amazon.com/sns/)
### Content
1. [Create SNS topic](10-SNS/10.1-CreateSNSTopic)
2. [Add Your Email Subscription](10-SNS/10.2-AddEmail)
