---
title: "WEEK 12 WORKLOG"
date: "2025-11-10"
weight: 2
chapter: false
pre: " <b> 1.12 </b> "
---

# **WEEK 12 WORKLOG**

### **Week 12 Objectives**

* Finalize and optimize the **AWS Application Load Balancer (ALB)** configuration.
* Learn and successfully configure advanced ALB features: **HTTP/2**, **WebSocket**, and **Sticky Sessions**.
* Conduct **Performance Testing** on the ALB to evaluate its load-handling capabilities.
* Complete the final workshop and prepare the final internship report.

---

### **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference/Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Mon) | **Configure HTTP/2**: Set up the ALB Listener (HTTPS) to support **HTTP/2**. Conduct initial research on **WebSocket**. | 24/11/2025 | 24/11/2025 | |
| 2 (Tue) | **Configure WebSocket**: Configure the ALB Listener to support **WebSocket** and test the connection. Optimize timeout settings. | 25/11/2025 | 25/11/2025 | |
| 3 (Wed) | **Configure Sticky Sessions (Part 1)**: Configure **Sticky Sessions** (Target Group Attributes) to maintain user sessions. Run **Health Checks**. | 26/11/2025 | 26/11/2025 | |
| 4 (Thu) | **Configure Sticky Sessions (Part 2)**: (Repeated) Verify and confirm that the Sticky Sessions feature is working correctly. | 27/11/2025 | 27/11/2025 | |
| 5 (Fri) | **Performance Testing**: Use a tool (JMeter/Gatling) to load test the ALB. Analyze the results and prepare the final report. | 28/11/2025 | 28/11/2025 | |

---

### **Week 12 Achievements**

* Successfully configured an **Application Load Balancer (ALB)** to support the **HTTP/2** protocol (via an HTTPS listener).
* Successfully configured the ALB to support **WebSocket** connections for real-time communication and troubleshot `idle timeout` issues.
* Configured and verified **Sticky Sessions** (Application-based cookie) on the Target Group, ensuring requests from a single client are routed to the same instance.
* Successfully ran **Health Checks** to ensure all instances in the Target Group were healthy and ready to receive traffic.
* Conducted **Performance Testing** against the ALB using load-generation tools (like JMeter/Gatling) to analyze key metrics (response time, error rate).
* Completed the final workshop and prepared the final summary report for the 12-week internship.