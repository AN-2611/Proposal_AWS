+++
title = "Config DNS Records"
date = 2022
weight = 13
chapter = false
pre = "<b>13. </b>"
+++
1. Go to **Route 53** dashboard. Choose **Hosted zones**
![Route 53 Dashboard](/images/13-ConfigDNS/01-Route53Dashboard.png)
2. On the **test.name.vn** detail page. Choose **Create record**:
3. Record details:
    - **Record name:** Leave this field blank. This signifies you are creating a record for the root domain (yourdomain.com).
    - **Record type:** A - Routes traffic to an IPv4 address and some AWS resources.
    - Turn on the **Alias** toggle switch
4. Route traffic to:
    - **Choose endpoint:** Select **Alias to Application and Classic Load Balancer.**
    - **Choose Region:** Select **us-east-1** region
    - **Choose load balancer:** Click in the text field and your **advanced-alb** should appear
![Route 53 Dashboard](/images/13-ConfigDNS/02-CreateRecord.png) 
5. While still in your hosted zone, click **Create record** again.
    - **Record details:**
        - **Record name:** `ws  `
        - **Record type:** CNAME - Routes traffic to another domain name.
        - **Value:** Paste the DNS name of your Application Load Balancer here. (You can find this on the EC2 > Load Balancers page)
        - **TTL (Seconds):** Leave the default of 300.
        - **Routing policy:** Simple routing.
        - Click **Create records.**
![Route 53 Dashboard](/images/13-ConfigDNS/03-CNAMERecords.png) 