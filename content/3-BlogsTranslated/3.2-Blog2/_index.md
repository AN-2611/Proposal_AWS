---
title: "Blog 2"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---


# Insights and learnings from Amazon Q in Connect at NatWest
by Prabhakar Rajasekar, Abhay Kumar, Georgina Williams, and Prateek Guleria | on 02 APR 2025 | in [Amazon Connect](https://aws.amazon.com/blogs/contact-center/category/messaging/amazon-connect/), [Amazon Q](https://aws.amazon.com/blogs/contact-center/category/amazon-q/), [Customer Solutions](https://aws.amazon.com/blogs/contact-center/category/post-types/customer-solutions/), [Generative AI](https://aws.amazon.com/blogs/contact-center/category/artificial-intelligence/generative-ai/), [Intermediate (200)](https://aws.amazon.com/blogs/contact-center/category/learning-levels/intermediate-200/), [Thought Leadership](https://aws.amazon.com/blogs/contact-center/category/post-types/thought-leadership/) | [Permalink](https://aws.amazon.com/blogs/contact-center/insights-and-learning-of-amazon-q-in-connect-at-natwest/)
Agents are critical components of any contact center, and it is essential for organisations to provide them with the right tools for success. By supporting agents effectively, companies not only improve the agent experience but also enhance the end-customer experience. To address this need, Amazon Connect offers [Amazon Q in Connect](https://aws.amazon.com/connect/q/), a generative AI assistant that provides real-time personalised recommendations to help agents perform their roles more efficiently and effectively.

To implement generative AI-powered agent assistance, you need to consider various factors such as your testing strategy and the impact to the agent experience. In this blog post, you will learn how NatWest Group, a major financial services institution, implemented Amazon Q in Connect. We’ll focus on the specific challenges encountered during user acceptance testing (UAT). These challenges include selecting the appropriate intents to test, integrating with legacy knowledge systems, and evaluating the success of the pilot. We will also share designed solutions to overcome some of these challenges.

## Solving key business problems with generative AI
[NatWest Group](https://www.natwestgroup.com/) is a UK-focused bank serving over 19 million customers, with businesses across retail, commercial and private banking markets.

By [leveraging Amazon Q in Connect](https://youtu.be/zbrLI6ktTcg?t=2623), NatWest planned to provide the right outcome or decision to the customer faster with a specific focus on agent compliance to process and procedure and reduction in Average Handle Time (AHT). This strategic implementation serves multiple purposes:

Immediate Benefits:
  - Faster resolution of customer inquiries
  - Reduced time spent per customer interaction
  - More efficient handling of customer requests
  - Enhanced adherence to standardised protocols and guidelines by agents, resulting in decreased misinformation and fewer customer complaints

Long-term Impact:
  - Improved Net Promoter Score (NPS) through enhanced customer satisfaction
  - Better overall customer experience

NatWest Group elected to validate outcomes of Amazon Q in Connect using a limited set of their most experienced agents within a single business division.

## Knowledge management integration
Amazon Q in Connect offers seamless integration capabilities with multiple backend systems through pre-built connectors, including native support for Salesforce and customer website integrations. In NatWest’s case, while they maintained their own knowledge management system, they opted for a streamlined approach during their pilot implementation by utilising Amazon S3 as their knowledge repository associated with Amazon Q in Connect.

## How NatWest tested Amazon Q in Connect

Organisations can use Amazon Q in Connect in the Amazon Connect agent workspace, partner desktops (like Salesforce) or in a customer contact control panel (CCP). NatWest decided to modify their existing CCP to integrate Amazon Q in Connect, which allowed them to quickly iterate on the existing desktop used by agents.
![/](/images/3-Blogs/Blog-2/Picture-1.png)


## Intent identification and mapping methodology
Given the variety of potential customer inquiries, it would be impractical to test every possible scenario during the initial pilot phase. Therefore, a strategic approach to identifying and prioritizing customer intents is essential.

NatWest adopted a focused methodology by:
  - Utilising Amazon Lex to analyze and identify the top 10 most common reasons for customer calls (intents)
  - Utilising Amazon Connect Contact Lens to identify corresponding customer transcript for testing
  - Selecting these high-frequency intents as primary test cases
  - Systematically matching relevant knowledge articles to each identified intent

This process follows two key steps:
  - Analysis of call data to identify and prioritise the most frequent customer inquiry types
  - Strategic mapping of appropriate knowledge articles to each prioritised intent
This targeted approach allows for efficient testing and optimisation of the system while addressing the most impactful customer scenarios first.

## Knowledge article optimisation
Knowledge articles are traditionally designed with contact center agents as the primary audience. However, Amazon Q in Connect takes a more comprehensive approach by analysing conversation dynamics from both sides – monitoring key phrases and trigger words from both customer interactions and agent responses to generate real-time, contextual assistance.

To optimise this capability, knowledge articles need to be adapted to work effectively with Amazon Q in Connect. Following [Amazon Q in Connect’s knowledge article best practices](https://aws.amazon.com/blogs/contact-center/optimizing-knowledge-base-amazon-q-in-connect/) enables organisations to restructure their existing content in a way that maximises the AI’s ability to provide relevant, real-time support during customer interactions.

This transformation of knowledge articles ensures the content is properly formatted and structured to take full advantage of generative AI-powered agent assistance tools.

## Balancing AI assistance with guided workflows
While generative AI for agent assistance is powerful, certain customer inquiries require a more structured approach through guided workflows. [Step-by-step guides](https://docs.aws.amazon.com/connect/latest/adminguide/step-by-step-guided-experiences.html) are particularly valuable for handling complex scenarios and regulated processes that demand precise procedural compliance.

It’s essential to evaluate and identify which knowledge articles are best suited for conversion into structured guides versus AI-assisted responses. The optimal solution leverages both approaches:
  - AI assistance for dynamic, straightforward inquiries
  - Guided workflows for complex, compliance-sensitive processes

Amazon Q in Connect enhances this dual approach by seamlessly integrating with step by step guides in Amazon Connect. This integration creates a comprehensive support system that combines the flexibility of AI with the precision of structured guides, delivering the most effective toolset for agents to handle customer inquiries efficiently and accurately.

## Evaluating the success of a proof of concept (PoC)
While the ultimate objectives of implementing agent assistance include reducing call handling time, improving agent adherence to right procedure and improving the NPS, measuring these metrics effectively in a small-scale pilot presented challenges.

To address this, NatWest Group decided to measure the success by manual agent evaluation of the outcome after every call. Instead of manually evaluating Amazon Q in Connect after every call, they implemented automatic reporting.

This automated reporting strategy enabled NatWest to:

  - Objectively track performance metrics
  - Gather meaningful data during the pilot phase
  - Evaluate the solution’s impact without adding burden to agents’ workload
![s](/images/3-Blogs/Blog-2/2025-03-31_11-03-26.png)

By developing custom reporting capabilities in addition to monitoring capability of Amazon Q in Connect, NatWest created a more systematic and data-driven approach to measuring the success of their agent assistance implementation, even within the constraints of a pilot.

## Customer reporting architecture
Reporting is essential in generative AI deployments to monitor both the quality and safety of AI-generated responses, ensuring accuracy while catching potential issues early. Unlike traditional software with deterministic behavior, generative AI systems require continuous monitoring to ensure they deliver value within acceptable parameters. Comprehensive reporting provides crucial metrics to justify ROI, identify optimization opportunities, and track adoption patterns. Ultimately, good reporting helps organisations maintain control while maximizing the benefits of their AI investment.
![s](/images/3-Blogs/Blog-2/CustomReportingBlog.png)

Some of the key points to note around this architecture as below:

  1. The custom UX in the agent’s browser invokes Amazon Q in Connect API to get customer’s query and suggestions from Amazon Q
  2. Custom UX invokes API Gateway REST endpoint to send collected data
  3. The API Gateway invokes a AWS Lambda function and passes on the data
  4. The AWS Lambda function invokes Amazon Comprehend service to redact PII and other sensitive data and then writes the redacted data to the Amazon DynamoDB table
  5. Reporting Lambda pulls data from the table
  6. Reporting Lambda sends email with the reports attached
## Successfully scaling Amazon Q in Connect
![s](/images/3-Blogs/Blog-2/2025-03-31_10-53-52-1.png)

This flow outlines the key steps and considerations for effectively scaling your Amazon QiC implementation for agent assistance and self-service.

## Conclusion
NatWest Group’s experimentation with Amazon Q in Connect in production demonstrates how financial institutions can effectively leverage generative AI to enhance their contact center operations. Through their methodical approach to testing and implementation, NatWest has shown that success depends on several key factors: strategic intent selection, optimised knowledge management, and robust measurement capabilities.

Their experience highlights the importance of:

  - Taking a focused approach to testing with experienced agents
  - Properly structuring knowledge articles for AI consumption
  - Balancing AI assistance with guided workflows for complex scenarios
  - Implementing systematic measurement approaches through reporting

As organisations look to implement similar solutions, NatWest’s journey offers valuable insights into how to approach implementation, testing, and scaling of AI-powered agent assistance tools in contact center environments.

## Author

{{< author-bio img="/images/3-Blogs/Blog-2/Prateek-copy.jpg" name="Prateek Guleria" >}}
 **Prateek Guleria** is a DevOps Lead at Natwest. Entrusted with performing automations, overseeing the development and implementation of CI/CD pipelines, and maintaining cloud infrastructure on AWS platform.
{{< /author-bio >}}

{{< author-bio img="/images/3-Blogs/Blog-2/Georgina.jpeg" name="Georgina Williams" >}}
Based in London as a Customer Experience (CXE) Principal Specialist, **Georgina Williams** supports large global organisations transform their customer experience strategies. Outside of work she enjoys spending time with her 2 young daughters on crafting projects.
{{< /author-bio >}}

{{< author-bio img="/images/3-Blogs/Blog-2/Prabha.png" name="Prateek Guleria" >}}
**Prabhakar Rajasekar** is a Specialist Customer Experience (CXE) Solution Architect at Amazon Web Services for WWSO in Aachen, Germany. Besides helping customers in their digital transformation, you will see him spending time with his kids in the garden or in the woods.
{{< /author-bio >}}

{{< author-bio img="/images/3-Blogs/Blog-2/Abhay-copy.jpeg" name="Prateek Guleria" >}}
**Abhay Kumar** is a Director of Engineering at Natwest. He is responsible for Architecture, Development, Maintenance, Quality, and Security of the Contact Centre Platform.
{{< /author-bio >}}