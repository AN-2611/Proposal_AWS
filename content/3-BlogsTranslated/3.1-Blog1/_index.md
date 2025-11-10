---
title: "Blog 1"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---


# Intelligent coding at your fingertips: Introducing an agentic coding experience in your IDE

by Brian Beach | on 05 MAY 2025 | in [Amazon Q](https://aws.amazon.com/blogs/devops/category/amazon-q/), [Amazon Q Developer](https://aws.amazon.com/blogs/devops/category/amazon-q/amazon-q-developer/), [Announcements](https://aws.amazon.com/blogs/devops/category/post-types/announcements/) | [Permalink](https://aws.amazon.com/blogs/devops/amazon-q-developer-agentic-coding-experience/) |

Back in March, I wrote about the [new agentic coding experience within the Amazon Q Developer CLI](https://aws.amazon.com/blogs/devops/introducing-the-enhanced-command-line-interface-in-amazon-q-developer/). Recently, [Amazon Q Developer](https://aws.amazon.com/q/developer/) announced that it has [added a similar experience to the integrated development environement (IDE)](https://aws.amazon.com/about-aws/whats-new/2025/05/amazon-q-developer-agentic-coding-experience-ide/). Agentic coding in the IDE allows you to work with Amazon Q Developer to read and write files locally, run bash commands, build code, and more in near real-time through natural language conversations. The new experience redefines how you write, modify, and maintain code by leveraging natural language understanding to seamlessly execute complex workflows. The new agentic coding experience is now available in VS Code with support in other IDEs coming soon.

---

## Background

Before I explain the new agentic coding experience, let’s take a minute to review the existing chat capabilities within the Amazon Q Developer IDE. As the name implies, the traditional chat allows me to have a conversation with Q Developer. This is a great option when I’m learning and planning. It provides a natural back-and-forth dialogue. Personally, I like the traditional chat during the planning phase of the Software Development Lifecycle (SDLC). I can chat with Q Developer to discuss my architecture and the various tradeoffs of different designs before I start working.

However, once I move into the build phase of the SDLC, I prefer the new agentic coding experience. In this new experience, Q Developer can do so much more than just have a conversation. It can directly interact with the development environment, reading and writing files, using various development tools, and even querying AWS resources. This allows for a far more dynamic, hands-on coding workflow compared to the traditional chat interface.

Rather than just discussing requirements, the agentic agent can take direct action to implement them. It can scaffold new projects, update existing code, and provide step-by-step summaries of its progress – all through a seamless, conversational interface right within the IDE. The great news is that I now have both options available to me. I can simply toggle between a traditional chat in the planning phase, and the new agentic coding in the build phase.

## Walkthrough
Let’s walk through a simple example using the [AWS Cloud Development Kit (CDK)](https://aws.amazon.com/cdk/). I love CDK, and I use it all the time in my role. However, let’s assume that I don’t have a lot of experience, and want to learn more about CDK before I start using it. Since I just want to learn, I’ll start in the traditional chat experience, and ask Q Developer “How do I create an new CDK app?” As you can see in the following image, Q Developer starts to teach me about CDK. Along with the instructions, Q provides commands that I could copy and paste into my shell to get started.![.](/images/3-Blogs/Blog-1/ide-agentic-coding-01.png)

While this is a great, I am already familiar with CDK. I don’t need to learn how to create a new application. I am ready to start building! Therefore, I will toggle from traditional chat to agentic coding by clicking on the angle bracket pair in the bottom left corner of the chat window. Then, I will ask Q Developer to “Create a new CDK app in this folder using TypeScript.” First, notice that I am not asking a question like I did previously, but I am giving a command. In the following image, you can see that Q Developer is acting on my command rather that teaching me what to do.
![.](/images/3-Blogs/Blog-1/ide-agentic-coding-02.png)

This is the power of the new agentic coding. It is not simply teaching me how to create a CDK app. Amazon Q Developer is creating the app for me. There are a few important things that I want to call out here. First, Amazon Q Developer can use tools when it is running agentic coding mode. In this example, Q is using a series of shell commands — <span class="highlight-code"> mkdir, cd, npx, npm, etc.</span> — to create the CDK app. I will discuss other tools later in this post. Second, Q Developer is asking my permission before it runs these commands. This allows me to retain control over the development process. I’ll click the Run button and allow Q to create the new application resulting in the following project structure.
![.](/images/3-Blogs/Blog-1/ide-agentic-coding-03.png)

It’s easy to overlook the power of allowing Q Developer to use tools. By using shell commands, it was able to generate the project using the latest template, and install dependencies for me. Running shell commands is just one of many changes with the agentic coding experience. Next, let’s look at how code generation works in agentic coding.

## Code Generation
Amazon Q Developer has been generating code since it [first launched in June of 2022](https://aws.amazon.com/about-aws/whats-new/2022/06/aws-announces-amazon-codewhisperer-preview/). Since then, Amazon Q Developer has evolved, adding new features over time. Code generation began with [inline suggestions](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/inline-suggestions.html), followed by [chat](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/q-in-IDE-chat.html), and [the agent for software developmen](https://aws.amazon.com/blogs/devops/amazon-q-developers-new-context-features/). The new agentic coding, reinvents the code generation experience again. In the following example, I am going to add a Lambda function to the CDK stack that Q Developer created earlier. I ask Q Developer to “Add a new Lambda function that is triggered from the arrival of a file in an existing S3 bucket.”
![.](/images/3-Blogs/Blog-1/ide-agentic-coding-04.png)

Multiple important things happened in this example that I want to explain. First, notice that Q Developer edited the CDK Stack to add the new [AWS Lambda](https://aws.amazon.com/pm/lambda) function. Second, Q Developer used a shell command to create a new folder. Third, Q created a new file for the Lambda function. Forth, it updated the README file. Q took all four of these actions in response to a single prompt. In addition, note that Q Developer is providing a diff for each change, making it easy for me to review the changes. You can see an example of the changes it make to the README.md in the following image. Finally, note that I can undo any of the changes that Q Developer made along the way.

This is a big improvement over the traditional chat experience. Now let’s look at how Q Developer can describe my AWS resources.

## Describing AWS resources
Remember that I am building an application that is triggered by the arrival of a file in an existing [Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/) bucket. In the prior example, you can see that I need to pass the name of the bucket in the <span class="highlight-code">ExistingBucketName</span> parameter when deploying the stack.

Let’s assume that I have forgotten the name of the bucket I want to use. The new agentic coding experience can help me with this too. In the following example, I ask Q to “List my S3 buckets in the ca-central-1 region?” Once again, Q Developer asks for permission to use the shell. After I accept, Q Developer uses the AWS CLI and lists the buckets I have available in Canada (ca-central-1).
![.](/images/3-Blogs/Blog-1/ide-agentic-coding-06.png)

With the name of the bucket, I am ready to deploy my stack. Of course, there still more work to do, but I’ll leave that for another post.

## Conclusion
The new agentic coding experience within the Amazon Q Developer IDE represents a significant step forward in integrating powerful AI-driven capabilities directly into the developer’s workflow. By enabling the coding agent to read, write, and execute code locally, access tools, and interact with AWS resources, Q Developer promises to dramatically streamline and enhance the coding process. You can visit the [Amazon Q Developer User Guide](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/getting-started-q-dev.html) to install the IDE and start leveraging the new agent chat for free. Give it a try and let me know what you think!

TAGS: [Developer Tools](https://aws.amazon.com/blogs/devops/tag/developer-tools/), [Development](https://aws.amazon.com/blogs/devops/tag/development/)