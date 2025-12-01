+++
title = "Performance Testing"
date = 2022
weight = 16
chapter = false
pre = "<b>15. </b>"
+++
1. We will use System Manager to conntect to **web-sg** instances like step **14. Check result**
2. Update the system and install Java:
```bash
sudo yum update -y
sudo dnf update -y
sudo yum install -y java-11-amazon-corretto
```
3. Download the latest version of JMeter (check the official website for the latest link):
```bash
sudo cd /home/ssm-user
sudo mkdir jmeter_tests
sudo cd jmeter_tests
sudo wget https://dlcdn.apache.org//jmeter/binaries/apache-jmeter-5.6.3.tgz
```
4. Extract the file
```bash
sudo tar -xzf apache-jmeter-5.6.3.tgz
```
5. It's easiest to create the test plan on your local computer using the JMeter GUI and then upload it to the server. You should refer to the following articles:
   - [Install Java on Windows, Linux and macOS](https://www.geeksforgeeks.org/linux-unix/download-install-java-windows-linux-macos/)
   - [Install Apache JMeter on Windows](https://www.geeksforgeeks.org/installation-guide/how-to-install-apache-jmeter-on-windows/)
6. On your local machine, open JMeter. Create a simple **Test Plan**:
   - Right-click on Test Plan -> **Add** -> **Threads (Users)** -> **Thread Group.**
     - **Number of Threads (users):** The number of concurrent users (e.g., 100).
     - **Ramp-up period (seconds):** How long to take to start all threads (e.g., 10).
     - **Loop Count:** How many times each thread will run the test. Choose **Infinite**
![Thread Group](/images/15-PerformanceTesting/01-ThreadGroup.png)
   - Right-click on Thread Group -> **Add** -> **Sampler** -> **HTTP Request.**
     - **Protocol:** http or https.
     - **Server Name or IP:** Paste your domain name **test.name.vn**. Do not use the IP of an individual instance.
     - **Path:** The API endpoint or page you want to test. In this case, leave default
![Thread Group](/images/15-PerformanceTesting/03-HTTPRequest.png)
7. Save the Test Plan as a .jmx file (e.g., web-service-test.jmx).
8. Navigate **S3** to create bucket namely: `testing-plan-946` then upload the file
![Thread Group](/images/15-PerformanceTesting/04-CreateBucket.png)
9. From the SSM Session Manager session on EC2, download the file from S3:
```bash
sudo aws s3 cp s3://testing-plan-946/web-service-test.jmx /home/ssm-user/jmeter_tests
```
10.  In your SSH session on EC2, navigate to the JMeter bin directory.
```bash
cd /home/ssm-user/jmeter_tests/apache-jmeter-5.6.3/bin/
```
11.  Run the test using non-GUI mode:
```bash
./jmeter -n -t /home/ssm-user/jmeter_tests/web-service-test.jmx -l /home/ssm-user/jmeter_tests/web-service-results.csv
```
12. With 748.324 traffic, the CPU soared quickly 99.05%
![Thread Group](/images/15-PerformanceTesting/05-HighCPU.png)
13. You are also see charts in CloudWatch Dashboard
![Thread Group](/images/15-PerformanceTesting/06-CWDashboard-2.png)
14. Soon you will receive a warning email 
![Thread Group](/images/15-PerformanceTesting/07-Email.png)