---
title : "Registering a Domain with Amazon Route 53"
date : "2025-10-10"
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---
1. Sign in to the [AWS Management Console](https://aws.amazon.com/console/).
2. In the top search bar, type `Route 53` and select the **Route 53** service from the results.

![search-route53](/images/2-Preparation/2.1-RegisterDomain/01-searchRoute53.png)


3. In the Route 53 dashboard, click on **Registered domains** in the left-hand navigation menu.
4. Click the **Register domain** button.
![Route53-Dashboard](/images/2-Preparation/2.1-RegisterDomain/02-Route53Dashboard.png)

5. In the **Choose a domain name** field:
    - Enter the domain name you wish to register. In this lab, we use domain `test.name.vn` .
    - Click the **Search** button to see if the domain is available.
    - If the domain is available, it will appear in the **Search result** list with its annual registration price. Click **Proceed to checkout.**
![Register-Domain](/images/2-Preparation/2.1-RegisterDomain/03-RegisterDomains.png)
6. In the **Checkout** field, remember disable **Auto-renew** feature if you don't want to pay any using fee after your domain is expired. Click **Next** to move to the next step.

![Pricing](/images/2-Preparation/2.1-RegisterDomain/04-CheckoutPricing.png)

7. On the **Contact details for your domain** page, fill out the information.
    {{% notice info %}} 💡**Important**: Ensure you enter a valid and accessible email address. AWS will send a mandatory verification link to this address.
    {{% /notice %}}

![Contact-Information](/images/2-Preparation/2.1-RegisterDomain/05-ContactInfo.png)

1. On the **Review and complete your order** page:
    - Carefully check whether your infomation is wrong
    - Check the box to confirm you have read and agree to the **Terms and conditions** 
    - Click **Submit** to finalize the purchase.
    - Shortly after completing the order, AWS will send a verification email to the your address. Open this email and click the verification link inside.
![Contact-Information](/images/2-Preparation/2.1-RegisterDomain/06-ReviewInfo.png)
1. When you registry a domain sucessfully, AWS automatically create a public **Hosted Zone** 
    - In the Route 53 navigation pane, click **Hosted zones.**
    - You will see a new public Hosted Zone with the same name as the domain you just registered.