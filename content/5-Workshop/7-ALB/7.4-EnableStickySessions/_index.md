+++
title = "Enable Sticky Sessions"
date = 2022
weight = 5
chapter = false
pre = "<b>7.4 </b>"
+++
1. In the left-hand navigation pane, under **Load Balancing**, click on **Target Groups.**
![EC2 Dashboard](/images/7-ALB/7.4-EnableStickySessions/01-EC2Dashboard.png)
2. From the list of target groups, check the box next to your **web-tg**. Click on the Actions dropdown menu at the top right. Select **Edit attributes.**
![web-tg check the box](/images/7-ALB/7.4-EnableStickySessions/02-webtgActionDropdown.png)
3. On the **Edit attributes** page, find the **Stickiness** section.
   - Check the box to **Turn on stickiness**.
   - **Stickiness duration**: Enter 1 and select days from the dropdown menu.
   - **Stickiness type:** Load balancer generated cookie.
   -  Click the **Save changes** button.
![Enable Stickiness](/images/7-ALB/7.4-EnableStickySessions/03-TurnOnStickiness.png)