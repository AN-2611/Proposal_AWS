+++
title = "Initialize CloudWatch Alarms"
date = 2022
weight = 11
chapter = false
pre = "<b>11. </b>"
+++
### Introduce
![iconASG](/images/11-CW/icon.png)
**Amazon CloudWatch** is AWS's native monitoring and observability service. It provides you with the data and actionable insights to monitor your applications, understand system-wide performance changes, and respond to operational health issues.

We will use two key features of CloudWatch:

- Alarms: An alarm watches a single metric and performs an action when that metric breaches a defined threshold. This is our proactive defense, automatically notifying us via the **alb-alerts** SNS topic when something goes wrong, like a server becoming unhealthy or response times getting too high.

- Dashboards: A dashboard is a customizable page in the CloudWatch console where you can create a single, consolidated view of your application's most important metrics. This gives you an "at-a-glance" visual overview of your system's health and performance in real-time.
### Cost
- [AWS CloudWatch Pricing](https://aws.amazon.com/cloudwatch/pricing/)

### Documentation
- [AWS CloudWatch](https://docs.aws.amazon.com/cloudwatch/)

### Content
1. [Create the Unhealthy Hosts Alarm](11-CW/11.1-UnhealthyAlarm)
2. [Create the High CPU Alarm](11-CW/11.2-HighResponseAlarm)
3. [Create CloudWatch Dashboard](11-CW/11.3-CreateCloudWatchDashboard)