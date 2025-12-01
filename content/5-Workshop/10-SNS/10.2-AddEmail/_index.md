+++
title = "Add Your Email Subscription"
date = 2022
weight = 3
chapter = false
pre = "<b>10.2 </b>"
+++
1. You should now be on the details page for your new alb-alerts topic.
2. In the **Subscriptions tab**, click the **Create subscription** button.
![SNS Dashboard](/images/10-SNS/10.2-AddEmail/01-SNSDashboard.png)
3. Configure Subscription Details:
    - **Topic ARN:** This will be pre-filled with the ARN for **alb-alerts.**
    - **Protocol:** select Email.
    - **Endpoint:** Enter the email address where you want to receive alerts
![Email Subscription](/images/10-SNS/10.2-AddEmail/02-Sub.png)
4. Open this email and click the "Confirm subscription" link. The status of your email subscription should change from **Pending confirmation** to **Confirmed**.