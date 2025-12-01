---
title : "Request SSL Certificate"
date : "2025-10-10"
weight : 4
chapter : false
pre : " <b> 4.1 </b> "
--- 
1. In the search bar, type `Certificate   ` choose **ACM**
![Find ACM](/images/4-ACM/01-Find.png)
1. Click **Request a certificate**
2. In the **Requet certificate**, choose **Request a public certificate**. Then, click **Next**
![Domain Name](/images/4-ACM/02-RequestCert.png)
1. In the **Request public certificate**:
   - Under Fully qualified domain name, enter your main domain.
   - Click the **Add another name** to this certificate button to add a wildcard. This will secure all subdomains under your primary domain.
Example: `*.yourdomain.com`
![Domain Name](/images/4-ACM/03-DomainName.png)
1. Leave the other options as their defaults and click Request.
2. Click to the certificate you created. This action move you to the detail, Choose **Create record in Route 53**
![Cert Detail](/images/4-ACM/04-DetailsCert.png)
3. A confirmation page will appear. Review the records and click **Create records**. ACM automatically add the necessary CNAME records to your domain's hosted zone in Route 53.
![Review Record](/images/4-ACM/05-ReviewRecords.png)
4. Once AWS successfully verifies DNS records, the certificate **Status** will change from **Pending validation** to **Issued** in green
![Success](/images/4-ACM/06-Success.png)