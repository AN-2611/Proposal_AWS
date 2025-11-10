---
title: "Blog 4"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 3.4. </b> "
---

# Improving network observability with new AWS Outposts racks network metrics
<span class="meta-info">by Adam Duffield | on 06 AUG 2025 | in</span> [Advanced (300)](https://aws.amazon.com/blogs/compute/category/learning-levels/advanced-300/), [Announcements](https://aws.amazon.com/blogs/compute/category/post-types/announcements/), [AWS Outposts](https://aws.amazon.com/blogs/compute/category/compute/aws-outposts/), [AWS Outposts rack](https://aws.amazon.com/blogs/compute/category/compute/aws-outposts/aws-outposts-rack/)  | [Permalink](https://aws.amazon.com/blogs/publicsector/integrate-ai-powered-coding-assistance-in-secure-environments-using-continue-and-amazon-bedrock/) 

With [AWS Outposts racks](https://aws.amazon.com/outposts/rack/), you can extend AWS infrastructure, services, APIs, and tools to on-premises locations. Providing performant, stable, and resilient network connections to both the parent AWS Region as well as the local network is essential to maintaining uninterrupted service.

The release of two new [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) metrics, <span class='highlight-code'>VifConnectionStatus</span> and <span class='highlight-code'>VifBgpSessionState</span>, gives you greater visibility into the operational status of the Outpost network connections. In this post, we discuss how to use these metrics to quickly identify network disruptions, using additional data points that can help reduce time to resolution.

## Outposts network connectivity overview
When connecting an Outposts rack to your chosen data center location, network connections are made between the Outpost Networking Devices (ONDs) and Customer Network Devices (CNDs). These network connections support both the [Service Link](https://docs.aws.amazon.com/outposts/latest/userguide/region-connectivity.html) connectivity back to the chosen anchor Region and connectivity to the on-premises local network through the [Local Gateway](https://docs.aws.amazon.com/outposts/latest/userguide/outposts-local-gateways.html). [First-generation Outposts racks](https://aws.amazon.com/blogs/aws/aws-outposts-now-available-order-your-racks-today/) include a minimum of two network devices to provide resilience, with [second-generation Outposts racks](https://aws.amazon.com/blogs/aws/announcing-second-generation-aws-outposts-racks-with-breakthrough-performance-and-scalability-on-premises/) including four network devices.

[Virtual interfaces (VIFs)](https://docs.aws.amazon.com/outposts/latest/network-userguide/vif-vif-groups.html) are used to establish IP network connectivity between the Outpost and CNDs, using Border Gateway Protocol (BGP) for dynamic routing. You can view the details for these VIFs on the Outposts console by choosing Link aggregation groups (LAGs) in the navigation pane and drilling down to find the specific service link and local gateway VIF information. For each connection between an OND and CND, two BGP sessions are established: one to support service link traffic and the other to support local gateway traffic.

The following diagram shows an example of this connectivity for a first-generation Outposts rack.

![Figure 1: First-Generation Outposts Rack network connections](/images/3-Blogs/Blog-4/image-1-29.png)
<span class="meta-info">*Figure 1: First-Generation Outposts Rack network connections*</span>

In this configuration, a total of four VIFs are configured into two link aggregation groups (LAGs): one on each OND for the service link and local gateway VIFs.
## Understanding the new CloudWatch metrics for Outposts
Observability into the operational status of Outposts rack, including the status and performance of network connectivity, is important for you to be able to quickly identify and investigate potential issues. With the addition of the <span class='highlight-code'>VifConnectionStatus</span> and <span class='highlight-code'>VifBgpSessionState</span> Outposts metrics in CloudWatch, you have greater visibility into the connection status of the Outposts rack to your CNDs. The VifConnectionStatus metric is provided on a per-VIF level, available for both the local gateway and service link VIFs. It provides an indication on the status of the VIF using two possible values:

- A value of 1 indicates that the VIF is successfully connected to the CND with established BGP sessions and able to transmit traffic
- A value of 0 indicates that the VIF is not in an operational state due to an underlying issue

The <span class='highlight-code'>VifBgpSessionState</span> metric goes deeper into the BGP connectivity status between each Outposts VIF and CND. A BGP session can be in one of multiple states, each providing insight into where a potential issue might be. To reflect this, the CloudWatch metric value shown relates to the following BGP states:

1. IDLE – The initial state; the ONDs are waiting for a start event
2. Connect – The Outposts rack is waiting for the TCP connection to be complete
3. Active – The Outposts rack is trying to initiate a TCP connection
4. OpenSent – The router has sent an OPEN message and is waiting for a response
5. OpenConfirm – The router has received an OPEN message and is waiting for a KEEPALIVE response
6. Established – The BGP connection is fully established and the ONDs and CNDs can exchange routing information

With these metrics now available in CloudWatch, you can configure [Amazon CloudWatch alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) to alert when the metric values indicate potential issues. You can combine existing [CloudWatch metrics for Outposts](https://docs.aws.amazon.com/outposts/latest/userguide/outposts-cloudwatch-metrics.html) racks with these new metrics to give additional context and visibility into network connectivity status.
## Using CloudWatch metrics to investigate Outposts network connectivity issues
In the event of network connectivity issues, it’s important to understand how to use these metrics to assist with investigations and understand potential causes when seeing network impairment. To start with, the Configuration state of the VIFs should be checked. For each VIF, there are four possible states:

- Pending – A VIF is in this state from the time that it is created within a [VIF group](https://docs.aws.amazon.com/outposts/latest/network-userguide/vif-vif-groups.html) until the VIF becomes active on the OND
- Available – A VIF is active on ONDs
- Deleting – A VIF is in this state immediately after requesting deletion
- Deleted – A VIF is deleted
To check the state of an individual VIF on the Outposts console, choose Networking followed by Link aggregation groups (LAGS) in the navigation pane. The service link and local gateway VIFs associated with a specific LAG are shown, and when you choose a specific LAG, the configuration state of the associated VIFs are visible.

![Figure 2: AWS Outposts console showing VIF configuration details](/images/3-Blogs/Blog-4/image-2-23.png)
<span class="meta-info">*Figure 2: AWS Outposts console showing VIF configuration details*</span>

You can also retrieve these details programmatically. For example, use the following [AWS Command Line Interface (AWS CLI)](http://aws.amazon.com/cli) command to specifically check the configuration state of a service link VIF with ID <span class='highlight=code'>sl-vif-087faf21db43ba723</span>:
```
aws ec2 describe-service-link-virtual-interfaces /
--service-link-virtual-interface-id sl-vif-087faf21db43ba723
{
    "ServiceLinkVirtualInterfaces": [
        {
            "ServiceLinkVirtualInterfaceId": "sl-vif-087faf21db43ba723",
            "ServiceLinkVirtualInterfaceArn": "arn:aws:ec2:us-west-2:111122223333:service-link-virtual-interface/sl-vif-087faf21db43ba723",
            "OutpostId": "op-07f6f537e0607d3f1",
            "OutpostArn": "arn:aws:outposts:us-west-2:111122223333:outpost/op-07f6f537e0607d3f1",
            "OwnerId": "280066404755",
            "LocalAddress": "XX.XX.XX.XX/XX",
            "PeerAddress": " XX.XX.XX.XX/XX ",
            "PeerBgpAsn": 65000,
            "Vlan": 2006,
            "OutpostLagId": "op-lag-03782b844d7da1afc",
            "Tags": [],
            "ConfigurationState": "available"
        }
    ]
}
```
After confirming the Configuration state, you can use the <span class='highlight-code'>VifConnectionStatus</span> metric to determine the network connectivity status of individual VIFs. When operating and processing traffic in a healthy state, the value of this metric is 1. If this value changes to 0, it indicates a connectivity problem for that VIF between the Outpost and CNDs.

To further understand the potential cause of the VifConnectionStatus value, you can use the VifBgpSessionState metric. Under normal operational status, this metric value is 6, indicating that the BGP session is established and traffic can be sent and received. However, if this metric value changes to 1–5, then it is indicative of an issue. To start investigating the cause of this, you should review VIF configuration both on the Outposts console and programmatically. This includes the values set on the OND for VLAN, local and peer addresses, and BGP ASN. These values can be validated against the configuration on your on-premises CNDs if required. Furthermore, you can use the VifBgpSessionState metric value to determine the potential cause:

- If the value is 1, validate the values for BGP ASN and peer addresses
- If the value is 2, this might indicate port or IP address issues
- If the value is 3, this might indicate BGP version mismatches
- If the value is 4 or 5, this refers to networking path problems

By using a combination of these metrics, you can gain a clearer understanding of the potential network issue without having to engage with AWS or third-party support teams.

You can view and query these metrics on the CloudWatch console. In the navigation pane, choose All metrics, followed by Outposts under the AWS namespaces section. The Outposts namespace can only be viewed by the Outposts owner account, unless CloudWatch [cross-account observability](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch-Unified-Cross-Account.html) is configured. The new <span class='highlight-code'>VifConnectionStatus</span> and <span class='highlight-code'>VifBgpSessionState</span> metrics can be found under the <span class='highlight-code'>OutpostsID</span>, <span class='highlight-code'>VirtualInterfaceGroupId</span>, <span class='highlight-code'>VirtualInterfaceIInterfaceId</span> dimension.

![Figure 3: Amazon CloudWatch metrics for AWS Outposts](/images/3-Blogs/Blog-4/image-3-2.png)
<span class="meta-info">*Figure 3: Amazon CloudWatch metrics for AWS Outposts*</span>

For more information on working with metrics, see [Metrics in Amazon CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/working_with_metrics.html). For creating alerts based upon these new metrics and their values, refer to [Using Amazon CloudWatch alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html).

The resilient design of using multiple ONDs for both service link and local gateway traffic allows workloads to continue to run in the event of connectivity issues for single VIFs. For example, a single service link VIF might report as being down, but the remaining service link VIFs might be unaffected and remain available. In this scenario, the service link itself would remain functional and connected, albeit with potentially lower resilience and capacity. This can be validated throught the ConnectedStatus metric which would have a value of 1.

## Conclusion
This post provided details on the newly released CloudWatch metrics for Outposts racks, <span class='highlight-code'>VifConnectionStatus</span> and VifBgpSessionState, and how you can use them to investigate potential connectivity issues. For more information on Outposts rack networking patterns, see the [Networking](https://docs.aws.amazon.com/whitepapers/latest/aws-outposts-high-availability-design/networking.html) section of the Outposts High Availability Design and Architecture Considerations whitepaper. For more information about additional CloudWatch metrics that are available, check out the CloudWatch metrics for AWS Outposts documentation for [second-generation Outposts racks](https://docs.aws.amazon.com/outposts/latest/network-userguide/outposts-cloudwatch-metrics.html) and [first-generation Outposts racks](https://docs.aws.amazon.com/outposts/latest/userguide/outposts-cloudwatch-metrics.html).