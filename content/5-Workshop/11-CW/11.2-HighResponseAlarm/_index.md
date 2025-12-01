+++
title = "Create Request Count Alarm"
date = 2022
weight = 4
chapter = false
pre = "<b>11.2 </b>"
+++
1. Scroll down to **Metrics** from dropdown menu, click **All metrics** 
    - Navigate to **ApplicationELB** > **Per AppELB, per TG Metrics**
    - Find your **web-tg** and select the **RequestCountPerTarget** metric
    - Choose **Create alarms**
![EC2 Metric](/images/11-CW/11.2-HighResponseAlarm/01-CWDashboard.png)
1. Conditions:
    - **Threshold type:** Static
    - **Whenever RequestCountPerTarget is...:** Greater
    - **than...** 1000
![EC2 Metric](/images/11-CW/11.2-HighResponseAlarm/02-SpecifyMetric-2.png)
1. Click **Next**, configure the action to send a notification to your **alb-alerts** SNS topic, name the alarm `Web-Request-Count-Alarm`, and create it.
![EC2 Metric](/images/11-CW/11.2-HighResponseAlarm/03-AddAlarmDetails-2.png)
1. Repeat these steps as needed for your API and WebSocket target groups.