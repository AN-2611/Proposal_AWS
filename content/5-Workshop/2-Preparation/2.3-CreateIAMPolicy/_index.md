---
title : "Create IAM Policy "
date : "2025-10-10"
weight : 3
chapter : false
pre : " <b> 2.3 </b> "
---
Before attaching policies to the role, we'll first create our custom policy.
1. On the **Policies** page, right-click the **Create policy** button and open it in a new browser tab.
![Find Policies](/images/2-Preparation/2.3-CreateIAMPolicy/01-PoliciesDashboard.png)
2. In the **Specify permissions** page:
   - **Service:** S3
   - **Action allowed:** `GetObject` and `ListBucket`
   - **Resources**: `alb-access-logs-137`
![Find Policies](/images/2-Preparation/2.3-CreateIAMPolicy/02-ConfigPermiss.png)
3. Choose **Add more permission** to add SNS permission with `Publish   ` action allowed
![SNS policy](/images/2-Preparation/2.3-CreateIAMPolicy/06-SNSPolicy.png)

4. In the **Review and create**:
- **Policy name:** `S3-SNS-Policy`
- **Description:** `Grants read access to a specific S3 bucket and publish access to an SNS topic`
![Find Policies](/images/2-Preparation/2.3-CreateIAMPolicy/03-Review.png)
5. We need to attach the policy created to **CloudWatchAgentServerPolicy** role. Access to **CloudWatchAgentServerPolicy** role, choose **Add permission**
![Find Policies](/images/2-Preparation/2.3-CreateIAMPolicy/04-AddPermiss.png)
6. Typing `S3-SNS-Policy` to the search bar. Choose **Add permission**
![Find Policies](/images/2-Preparation/2.3-CreateIAMPolicy/05-AddPermissPage.png)