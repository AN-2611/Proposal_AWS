---
title: "Blog 3"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# Integrate AI-powered coding assistance in secure environments using Continue and Amazon Bedrock
<span class="meta-info">by Keith Boaman and Andrew Istfan | on 01 MAY 2025 | in</span> [Amazon API Gateway](https://aws.amazon.com/blogs/publicsector/category/application-services/amazon-api-gateway-application-services/), [Amazon Bedrock](https://aws.amazon.com/blogs/publicsector/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/), [Amazon Q](https://aws.amazon.com/blogs/publicsector/category/amazon-q/), [Amazon Q Developer](https://aws.amazon.com/blogs/publicsector/category/amazon-q/amazon-q-developer/), [Artificial Intelligence](https://aws.amazon.com/blogs/publicsector/category/artificial-intelligence/), [AWS Cloud Development Kit](https://aws.amazon.com/blogs/publicsector/category/developer-tools/aws-cloud-development-kit/), [AWS GovCloud (US)](https://aws.amazon.com/blogs/publicsector/category/public-sector/government/aws-govcloud-us/), [AWS Identity and Access Management (IAM)](https://aws.amazon.com/blogs/publicsector/category/security-identity-compliance/aws-identity-and-access-management-iam/), [AWS PrivateLink](https://aws.amazon.com/blogs/publicsector/category/networking-content-delivery/aws-privatelink/), [AWS Security Hub](https://aws.amazon.com/blogs/publicsector/category/security-identity-compliance/aws-security-hub/), [Developer Tools](https://aws.amazon.com/blogs/publicsector/category/developer-tools/), [Foundation models](https://aws.amazon.com/blogs/publicsector/category/artificial-intelligence/generative-ai/foundation-models/), [Government](https://aws.amazon.com/blogs/publicsector/category/public-sector/government/), [Public Sector](https://aws.amazon.com/blogs/publicsector/category/public-sector/), [Security, Identity, & Compliance](https://aws.amazon.com/blogs/publicsector/category/security-identity-compliance/), [Technical How-to](https://aws.amazon.com/blogs/publicsector/category/post-types/technical-how-to/) | [Permalink](https://aws.amazon.com/blogs/publicsector/integrate-ai-powered-coding-assistance-in-secure-environments-using-continue-and-amazon-bedrock/) 

![w](/images/3-Blogs/Blog-3/2..png)

Organizations adopting modern software development activities continue to embrace the advantages of AI and [large language models (LLMs)](https://aws.amazon.com/what-is/large-language-model/), maximizing the productivity of developers. [Amazon Q Developer](https://aws.amazon.com/q/developer/) provides you with an AI coding companion that delivers direct access for developers to the AI companion within the [integrated development environment (IDE)](https://aws.amazon.com/what-is/ide/).

Passing the context of relevant code from the IDE to an AI tool during software development offers massive productivity gains. However, it also opens the way for data spillage or release of proprietary information unless proper precautions are taken. Organizations that deploy in highly regulated environments, often in [Amazon Web Services (AWS)](https://aws.amazon.com/) GovCloud (US) [Regions](https://docs.aws.amazon.com/glossary/latest/reference/glos-chap.html#region), are looking for a way for their developers to securely use approved models outside Amazon Q that have appropriate guardrails and have the potential for customization.

In this post, we walk you through an example you can use leveraging the power of [Amazon Bedrock](https://aws.amazon.com/bedrock/) to provide a coding

## Architecture overview
At the time of this post’s publication, Amazon Q is not yet available in AWS GovCloud (US) Regions. However organizations can implement a robust alternative by combining the open source AI code assistant Continue with the serverless inference capabilities of Amazon Bedrock, both of which are fully supported in AWS GovCloud (US) Regions. This architecture uses Continue’s extensible framework to interface with Amazon Bedrock to create a secure, compliant AI coding assistant directly in your IDE. Although not discussed or evaluated as part of this example, alternative AI coding tools such as Cline or Aider could be opted for as well.

This example provides several key advantages:

  - Complete data sovereignty within AWS GovCloud (US) Regions
  - Customizable prompt engineering and model selection
  - Integration with existing IDE workflows
  - Ability to implement additional security controls and audit logging
  - Support for air-gapped environments through private API endpoints

By combining these components, organizations can provide their development teams with AI-assisted coding capabilities while maintaining the strict security and compliance requirements of AWS GovCloud (US) Region environments.

Authentication is completed through the standard AWS configuration file on your host machine. This example employs [AWS Identity and Access Management (IAM) Roles Anywhere](https://aws.amazon.com/iam/roles-anywhere/) to provide secure, automated credential management. By using X.509 certificates and a private certificate authority (CA), developers can obtain temporary AWS credentials without manual intervention.

In the following configuration, we show Visual Studio Code (VS Code) installed on a local workstation. Alternatively, the IDE can be installed on a virtual environment inside AWS, such as [Amazon AppStream 2.0](https://aws.amazon.com/appstream2/) or [Amazon Workspaces](https://aws.amazon.com/workspaces/) to have a preconfigured and scalable environment for developers or system administrators.

![Figure 1. High-level example architecture](/images/3-Blogs/Blog-3/1-10.png)
Figure 1. High-level example architecture

## Prerequisites
To deploy the example, you need access to [Amazon Bedrock foundation models (FMs)](https://aws.amazon.com/what-is/foundation-models/), which isn’t granted by default. You can request or modify access only by using the [Amazon Bedrock console](https://console.aws.amazon.com/bedrock/). 

Follow these steps:
  1. Sign in to the target AWS account with an IAM role that has [sufficient permissions](https://docs.aws.amazon.com/bedrock/latest/userguide/model-access-permissions.html) to manage access to FMs.
  2. Follow the instructions at Add or remove access to Amazon Bedrock foundation models.
  3. For this post, enable access to Anthropic’s Claude 3.0 Haiku and [Amazon Titan Text Express](https://aws.amazon.com/bedrock/amazon-models/titan/).

## Deployment walkthrough
To deploy the example, use the instructions in the following sections.
### Deploy IAM Roles Anywhere
You can use the Amazon Cloud Development Kit (AWS CDK) code written in Typescript at GitHub to deploy the configurations for AWS Private Certificate Authority, AWS Certificate Manager (ACM), IAM, and IAM Roles Anywhere. The code provided is an initial framework that can be adjusted as necessary. Next, we review some portions of the code.

In this example, AWS Private CA enables creation of Certificate Authority (CA) root and subordinate CAs without the investment and maintenance cost of operating and on-premise CA. The configuration of the root certificate within Private CA can be configured with the specifics for your organization.

![s](/images/3-Blogs/Blog-3/1.png)

From the root certificate in AWS Private CA, the AWS CDK will to create an example client certificate that can be installed on the client device. The client certificate will be passed through the IAM Roles Anywhere credential helper tool to allow the client to assume the role configured as part of IAM Roles Anywhere.

![j](/images/3-Blogs/Blog-3/3.png)

Below is a guideline to adjust and deploy the example code:
  1. Clone or download the repo locally.
  2. Navigate to the VSCodeBedrock folder.
![p](/images/3-Blogs/Blog-3/2-11.png)
  3. Adjust any settings in the lib/vs_code_ai-stack.ts file:
    
     * **Region:**
       * Set to 'us-gov-west-1' as example but can be changed to the desired target region.

     * **Root Certificate:**
       * templateARN: Change the partition if deploying outside of GovCloud
       * validity value: Adjust for certificate expiration requirements
     * **Client Certificate:**
       * domainName: Replace ‘your-domain.com’ with your desired domain name
       * subjectAlternativeNames: add any alterntiave names as desired
       * keyAlgorithm: Optional setting, default is RSA_2048
     * **Trust Policy for IAM Roles Anywhere**
       * String Condition: is set to string value for the aws-us-gov partition, change if deploying in different partition
     * **Profile for IAM Roles Anywhere:**
       * durationSeconds: how long before the authentication session should time out. Adjust as required.
     * **Deploy CDK via ‘cdk deploy’**

The created private certificate and associated private key can then be exported to the client devices certificate store that you want to establish the connection to Amazon Bedrock from. In the example we utilize [OpenSSL](https://www.openssl.org/) which is an open-source software library for Secure Sockets Layer (SSL) communication. Follow these steps:
  1. On the [ACM console](https://console.aws.amazon.com/certificate-manager/), select the private certificate to use on the local workstation.
  2. Set a private encryption passcode and generate Privacy Enhanced Mail (PEM) encodings.
  3. Download the exported certificate body, chain, and private key.
  4. Locally, decrypt the private key with OpenSSL. [[OpenSSL Compilation and Installation](https://wiki.openssl.org/index.php/Compilation_and_Installation)]

<span class="highlight-code">
openssl ec --passin pass:<encryptionpassphrase> -in private_key.pem -out private_key_decrypt.pem
</span>

We will allow the end user to assume an IAM through IAM Roles Anywhere and limit the permissions of the session to only call the APIs required for this particular use case. The below section of the CDK establishes the role and allows the role to be assumed by IAM Roles Anywhere:

![i](/images/3-Blogs/Blog-3/4.png)

### Set up Continue
To set up Continue, follow these steps:

  1. Download the Continue plugin for VS Code or JetBrains using the Continue homepage.
  2. After installing the Continue plugin, open the configuration file at <span class="highlight-code">~/.configure/config.json</span>. The configuration file can also be accessed by opening the Continue plugin, selecting the settings icon, and choosing Open configuration file at the top of the screen, as shown in the following screenshot.
![s](/images/3-Blogs/Blog-3/3-10-566x1024.png)
  3. Within the configuration file, modify the “models” object to contain the appropriate Amazon Bedrock models you wish to use. For more information on properly configuring Amazon Bedrock as a model provider for the plugin, refer to Amazon Bedrock under Model providers in the left navigation pane in the [Continue documentation](https://docs.continue.dev/customize/model-providers/bedrock).

![w](/images/3-Blogs/Blog-3/5.png)

### Enable AWS access
To enable AWS access, follow these steps:

  1. Install the AWS IAM Roles Anywhere credential helper from Get temporary security credentials from IAM Roles Anywhere. The credential helper is available for Windows, macOS, and Linux. SHA26 checksums are provided to verify the integrity of the download.
  2. Create a configured profile in ~/.aws/credentials that uses the recently installed signing helper in the following format. Continue will perform authentication to AWS with the credentials located in this file. Because the example uses IAM Roles Anywhere, this credential helper tool will automatically return the rotated credentials each time authentication is necessary, which means you avoid the hassle of modifying the credentials file each time tokens expire.
![p](/images/3-Blogs/Blog-3/6.png)
  3. Verify a successful connection by selecting your intended model and prompting your first question through Continue.

### Adapt to your environment
Although the current example provides a solid foundation for secure AI coding assistance, customers may desire additional network security measures to further enhance protection in highly regulated environments such as AWS GovCloud (US) Regions:

  1. [AWS PrivateLink](https://aws.amazon.com/privatelink/) can be used to create private, encrypted network connections between your virtual private cloud (VPC) and Amazon Bedrock. Aligning with the [Securely Access Services Over AWS PrivateLink](https://docs.aws.amazon.com/whitepapers/latest/aws-privatelink/aws-privatelink.html) whitepaper, this approach does the following:
     * Eliminates direct internet access to AI services
     * Reduces potential attack surfaces
     * Provides an additional layer of network isolation
  2. [Amazon API Gateway](https://aws.amazon.com/api-gateway/) can be used to employ these advanced security features:
     * Request [throttling](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-request-throttling.html) to prevent service abuse
     * Control and manage access
     * Integration with AWS WAF
  3. Leverage AWS Security Hub controls associated with implemented services

These modifications can help organizations meet stringent security requirements, including [National Institute of Standards and Technology (NIST)](https://aws.amazon.com/compliance/nist/), [Federal Risk and Authorization Management Program (FedRAMP)](https://aws.amazon.com/compliance/fedramp/), and Department of Defense (DoD) security standards by providing:

  * Least-privilege access controls
  * Comprehensive logging and monitoring
  * Encrypted service communications

By adopting these proposed network security enhancements, you can develop a more robust and secure approach to AI-assisted coding in highly regulated environments.

## Conclusion
This example demonstrates a practical approach to integrating AI-powered coding assistance in highly secure environments such as AWS GovCloud (US) Regions. By combining Continue, Amazon Bedrock, and IAM Roles Anywhere, you can achieve a framework that balances cutting-edge productivity with stringent security requirements.

This architecture provides organizations with a path to safely use AI technologies so developers enhance their productivity while maintaining comprehensive data sovereignty and compliance. As AI continues to transform software development, architectures like these will be critical in bridging innovation and security.

To learn more, visit [AWS in the Public Sector](https://aws.amazon.com/government-education/). For additional guidance, connect with your AWS solutions architect or contact us today!

TAGS: [Amazon API Gateway](https://aws.amazon.com/blogs/publicsector/tag/amazon-api-gateway/), [Artificial Intelligence](https://aws.amazon.com/blogs/publicsector/tag/artificial-intelligence/), [AWS GovCloud (US)](https://aws.amazon.com/blogs/publicsector/tag/aws-govcloud-us/), [AWS GovCloud (US) Region](https://aws.amazon.com/blogs/publicsector/tag/aws-govcloud-us-region/), [AWS IAM](https://aws.amazon.com/blogs/publicsector/tag/aws-iam/), [AWS PrivateLink](https://aws.amazon.com/blogs/publicsector/tag/aws-privatelink/), [AWS Public Sector](https://aws.amazon.com/blogs/publicsector/tag/aws-public-sector/), [government](https://aws.amazon.com/blogs/publicsector/tag/government/), [security](https://aws.amazon.com/blogs/publicsector/tag/security/), [technical how-to](https://aws.amazon.com/blogs/publicsector/tag/technical-how-to/)

![p](/images/3-Blogs/Blog-3/7.png)
<span class="highlight-code">

</span>