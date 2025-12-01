+++
title = "Create CloudWatch Dashboard"
date = 2022
weight = 5
chapter = false
pre = "<b>11.3 </b>"
+++
1. In the CloudWatch menu, click **Dashboards.**
2. Click **Create dashboard.**
![CW Dashboard](/images/11-CW/11.3-CreateCloudWatchDashboard/01-CWDashboard.png)
3. Dashboard name: `Application-Health-Dashboard`. Choose **Create dashboard**
4. Add **Widget:**
    - Click **Add widget**. Select **Line** graph. Click **Configure**.
    - Select **Metrics**, then navigate to **ApplicationELB** > **Per AppELB, per TG Metrics**
    - Select **RequestCountPerTarget** 
    - In the **Graphed metrics** tab, change the **Statistic** to **Sum**.
![CW Dashboard](/images/11-CW/11.3-CreateCloudWatchDashboard/02-ChangeStatistic.png)
1. Click to **+** button to add CPU Utilization widget:
![CW Dashboard](/images/11-CW/11.3-CreateCloudWatchDashboard/03-Button.png)
    - **Widget type:** Line
    - Choose **Next**
    - Go to **EC2** > By **Auto Scaling Group.**. Select **CPUUtilization** metric for all three of your Auto Scaling Groups.
    - Click **Create widget.**
![CW Dashboard](/images/11-CW/11.3-CreateCloudWatchDashboard/04-ChooseASG.png)

1. Continue click to **+** button to add Healthy Hosts Widget
    - **Widget type:** Line
    - Go to **ApplicationELB** > By **Per AppELB, Per TG Metrics.**. 
    - Select **UnHealthyHostCount** metric for all three of your target groups.
    - Click **Create widget.**
1. We created dashboard for RequestCountPerTarget, UnHealthyHostCount, CPUUtilization widget
![CW Dashboard](/images/11-CW/11.3-CreateCloudWatchDashboard/05-Result.png)