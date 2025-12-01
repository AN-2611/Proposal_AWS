+++
title = "Create the High CPU Alarm"
date = 2022
weight = 3
chapter = false
pre = "<b>11.1 </b>"
+++
1. Scroll down to **Metrics** from dropdown menu, click **All metrics** 
    - Navigate to **EC2** > **Auto Scaling Group**
    - Find your **web-service-asg** and select the **CPUUtilization** metric
    - Choose **Create alarms**
![EC2 Metric](/images/11-CW/11.1-HighCPUAlarm/06-CPUUtilization.png)
1. Conditions:
    - **Threshold type:** Static
    - **Whenever CPUUtilization is...:** Greater/Equal
    - **than...:** 80 (%)
![EC2 Metric](/images/11-CW/11.1-HighCPUAlarm/07-ConfigCPUUtilization.png)
1. Click **Next**, configure the action to send a notification to your **alb-alerts** SNS topic, name the alarm `Web-Service-High-CPU`, and create it.
![EC2 Metric](/images/11-CW/11.1-HighCPUAlarm/08-ConfigNoti.png)
1. Repeat these steps as needed for your API and WebSocket target groups
