+++
title = "Create EC2 Launch Template"
date = 2022
weight = 8
chapter = false
pre = "<b>8.1 </b>"
+++
1. In the AWS Management Console, go to the EC2 service.
2. In the left-hand navigation pane, scroll down and click on **Launch Templates**. Click the **Create launch template button**.
![EC2 Dashboard](/images/8-EC2LaunchTemplates/8.1-CreateEC2LaunchTemplate/01-EC2Dashboard.png)
3. Configure Template details:
   - **Launch template name**: `web-service-template`
   - **Template version description:** `Initial version for web servers`
   - Under Amazon Machine Image (AMI), search for **Amazon Linux 2**.
![AMI type](/images/8-EC2LaunchTemplates/8.1-CreateEC2LaunchTemplate/02-AMI.png)
   - Under **Instance type**, select **t3.medium** from the dropdown list.
   - Select an existing key pair from the dropdown. If you don't have one, you'll need to create it first. This is essential for accessing your instances via SSH if needed.
![Key pair](/images/8-EC2LaunchTemplates/8.1-CreateEC2LaunchTemplate/03-keypair.png)
{{% notice tip %}}
Do not have to specify the Subnet or Availability Zone (AZ) directly within the Launch Template itself. A Launch Template is a reusable blueprint. It's a best practice to omit network-specific details like subnets. Instead, you'll specify which subnets to use later when you create the Auto Scaling Group that uses this template. This makes your template more flexible
{{% /notice %}}

   - Under Network settings, ensure you do not select a subnet. Leave this blank.
   - For **Security groups**, do not use the default. Instead, search for and select the **web-sg** you created earlier.
![Networking ](/images/8-EC2LaunchTemplates/8.1-CreateEC2LaunchTemplate/04-Networking.png)
   - Expand the **Advanced details** section at the bottom.
   - Scroll down to find the IAM instance profile. Select the **RoleForEC2MonitoringUsingCloudWatchAgent** you created previously from the dropdown list.
![IAM role](/images/8-EC2LaunchTemplates/8.1-CreateEC2LaunchTemplate/05-IAMProfile.png)
   - Review the **Summary** panel on the right side to ensure all your settings are correct.
   - Click the **Create launch template** button.
1. Navigate to Launch Templates again.
   - Select the original **web-service-template**. 
   - Click **Actions** -> Modify template (Create new version)
![IAM role](/images/8-EC2LaunchTemplates/8.1-CreateEC2LaunchTemplate/06-ReuseTemplate.png)
   - Modify the following two fields:
     - **Launch template name:** `api-service-template`
     - **Template version description**: `Template for the backend API servers`
   - **Network settings:** Search for and select the **api-sg**.
1. Now, you'll repeat the exact same process for the WebSocket template.
2. Navigate to **Launch Templates** again.
   - Select the original **web-service-template**.
   - Click **Actions** -> **Create new template from selected**
   - Modify the following two fields:
     - **Launch template name:** `websocket-service-template`
     - **Template version description**: `Template for the backend Websocket servers`
     - **Security group:** Select **websocket-sg**.
3. Now, you have three Launch Template
![IAM role](/images/8-EC2LaunchTemplates/8.1-CreateEC2LaunchTemplate/07-Result.png)