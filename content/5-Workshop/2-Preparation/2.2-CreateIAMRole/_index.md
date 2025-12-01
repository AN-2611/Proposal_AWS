---
title : "Create IAM Role"
date : "2025-10-10"
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

In this step, we will proceed to create IAM Role. In this IAM Role, the policy **CloudWatchAgentServerPolicy** will be assigned, this is the policy that allows use Amazon CloudWatch Agent on servers.

1. In the top search bar, type `IAM` and select the **IAM** service from the results.
![role](/images/2-Preparation/2.2-CreateIAMRole/01-SearchIAM.png)
2. In the left navigation bar, click **Roles** and then **Create Role**
![IAM Dashboard](/images/2-Preparation/2.2-CreateIAMRole/02-AccessIAMDashboard.png)
3. In the **Select trusted entity** field:
     - Trusted entity type: **AWS service**
     - Service or use case: **EC2**
     - Use case: **EC2**
![Trusted Entity](/images/2-Preparation/2.2-CreateIAMRole/03-SelectTrustedEntity.png)
4. In the **Add permission** field:
    - Type `CloudWatchAgentServerPolicy` in the search bar
    - Choose this Policy
![Add permission](/images/2-Preparation/2.2-CreateIAMRole/04-AddPermission.png)
5. In the **Name, review, and create** field:
    - Role name: `RoleForEC2MonitoringUsingCloudWatchAgent`
    - Click **Create role** to complete the step
    - You should check carefully steps to ensure that there no error will happend
![Check again](/images/2-Preparation/2.2-CreateIAMRole/05-ReviewAgain.png)