💰 AWS Automated Cloud Cost Controller

A fully automated cloud cost optimization project that identifies idle Amazon EC2 instances using CloudWatch metrics and automatically stops them to avoid unnecessary AWS charges — powered by AWS Lambda, Amazon EventBridge, Amazon SNS, and IAM.

🛠️ Tech Stack

AWS EC2
AWS Lambda (Python)
Amazon CloudWatch
Amazon EventBridge (Scheduler)
Amazon SNS
IAM Roles & Policies
Serverless Architecture

📌 Project Use Case

In many cloud environments, EC2 instances are left running even when they are not actively used, which results in unnecessary cloud costs. This project helps you:

✅ Automatically stop idle EC2 instances
✅ Reduce AWS cloud expenses
✅ Eliminate manual monitoring
✅ Receive email notifications when actions are taken

🧠 How It Works

EventBridge triggers the Lambda function on a fixed schedule
→ Lambda fetches EC2 CPU utilization metrics from CloudWatch
→ If CPU usage is below the defined threshold
→ EC2 instance is stopped automatically
→ SNS sends an email notification
→ Done!

📐 Architecture Overview

+---------------------+ Scheduled Trigger +-----------------------+
| EventBridge | --------------------------> | AWS Lambda |
| (Rate-based Rule) | | (Idle EC2 Checker) |
+---------------------+ +-----------+-----------+
|
| CloudWatch Metrics
▼
+---------------------+
| Amazon EC2 |
| (Idle Instance) |
+---------------------+
|
| SNS Publish
▼
+---------------------+
| Amazon SNS |
| (Email Alerts) |
+---------------------+
|
Email Notification Sent

📦 Setup Guide

🔹 1. Create an EC2 Test Instance
Launch an EC2 instance using Amazon Linux and keep it idle without any workload.

📸 Screenshot: EC2 instance running

🔹 2. Create SNS Topic
Go to Amazon SNS → Create topic
Choose Standard
Name: ec2-idle-alerts

📸 Screenshot: SNS topic created

🔹 3. Subscribe an Email to SNS
Inside the SNS topic → Create subscription
Protocol: Email
Endpoint: Your email address
Confirm the subscription from your inbox

📸 Screenshot: Email subscription confirmed

🔹 4. Create IAM Role for Lambda
Create an IAM role for Lambda and attach permissions for EC2, CloudWatch, and SNS access.

📸 Screenshot: IAM role permissions

🔹 5. Create Lambda Function
Create a Lambda function using Python runtime.
Attach the IAM role and add logic to check EC2 CPU usage and stop idle instances.

📸 Screenshot: Lambda code and deployment

🔹 6. Create Scheduled Rule (EventBridge)
Create an EventBridge rule using the visual rule builder.
Configure a rate-based schedule (for example: every 30 minutes).
Set the Lambda function as the target.

📸 Screenshot: EventBridge rule configuration

✅ Testing the System

Keep the EC2 instance idle
Wait for EventBridge to invoke the Lambda function
Verify EC2 state change from Running → Stopped
Check Lambda logs in CloudWatch
Confirm SNS email notification

📸 Screenshot: EC2 stopped
📸 Screenshot: Lambda logs
📸 Screenshot: Email alert

📈 Outcome

The project successfully automated the detection and stopping of idle EC2 instances, reducing unnecessary cloud costs and manual operational effort.

🔮 Future Enhancements

Add tag-based protection for production instances
Calculate estimated cost savings
Automatically restart instances during business hours
Extend support for multi-account environments

🏁 Conclusion

This project provided hands-on experience with AWS automation, serverless architecture, cloud monitoring, and cost optimization. It demonstrates how real-world cloud challenges can be solved using AWS-native services.

🧑‍💻 Author

Your Name
GitHub: your-github-link
LinkedIn: your-linkedin-link
