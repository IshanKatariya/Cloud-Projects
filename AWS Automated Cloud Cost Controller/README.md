## 💰 AWS Automated Cloud Cost Controller

A fully automated cloud cost optimization project that identifies idle Amazon EC2 instances using CloudWatch metrics and automatically stops them to avoid unnecessary AWS charges — all powered by AWS Lambda, Amazon EventBridge, Amazon SNS, and IAM.

## 🛠️ Tech Stack

AWS EC2

AWS Lambda (Python)

Amazon CloudWatch

Amazon EventBridge (Scheduler)

Amazon SNS

IAM Roles & Policies

## 📌 Project Use Case

In many cloud environments, EC2 instances are left running even when they are not actively used, which results in unnecessary cloud costs. This project helps you:

✅ Automatically stop idle EC2 instances
✅ Reduce AWS cloud expenses
✅ Eliminate manual monitoring
✅ Receive email notifications when actions are taken

## 🧠 How It Works

EventBridge triggers the Lambda function on a fixed schedule
→ Lambda fetches EC2 CPU utilization metrics from CloudWatch
→ If CPU usage is below the defined threshold
→ EC2 instance is stopped automatically
→ SNS sends an email notification
→ Done!

## 📐 Architecture Overview
+---------------------+        Scheduled Trigger        +-----------------------+
|   EventBridge       |  -------------------------->  |     AWS Lambda        |
| (Rate-based Rule)   |                                | (Idle EC2 Checker)    |
+---------------------+                                +-----------+-----------+
                                                                |
                                                                | CloudWatch Metrics
                                                                ▼
                                                      +---------------------+
                                                      |     Amazon EC2      |
                                                      |  (Idle Instance)    |
                                                      +---------------------+
                                                                |
                                                                | SNS Publish
                                                                ▼
                                                      +---------------------+
                                                      |     Amazon SNS      |
                                                      |  (Email Alerts)     |
                                                      +---------------------+
                                                                |
                                                      Email Notification Sent

## 📦 Setup Guide
🔹 1. Create an EC2 Test Instance

Launch an EC2 instance using Amazon Linux

Keep the instance idle (no workload)

📸 Screenshot: EC2 instance running

🔹 2. Create SNS Topic

Go to Amazon SNS → Create topic

Choose Standard

Name: ec2-idle-alerts

📸 Screenshot: SNS topic created

🔹 3. Subscribe Email to SNS

Open the SNS topic

Create subscription

Protocol: Email

Endpoint: your email

Confirm subscription from inbox

📸 Screenshot: Email subscription confirmed

🔹 4. Create IAM Role for Lambda

Attach the following permissions:

AmazonEC2FullAccess

CloudWatchReadOnlyAccess

AmazonSNSFullAccess

📸 Screenshot: IAM role permissions

🔹 5. Create Lambda Function

Runtime: Python

Attach the IAM role

Add logic to:

Read CPU metrics

Stop idle EC2 instances

Send SNS email

📸 Screenshot: Lambda code & deployment

🔹 6. Create Scheduled Rule (EventBridge)

Create a rule using Visual Rule Builder

Schedule expression:

rate(30 minutes)


Target: Lambda function

📸 Screenshot: EventBridge rule configuration

## ✅ Testing the System

Keep EC2 instance idle

Wait for EventBridge to trigger Lambda

EC2 state changes from Running → Stopped

Verify:

Lambda logs (CloudWatch)

SNS email notification

📸 Screenshot: EC2 stopped
📸 Screenshot: Lambda logs
📸 Screenshot: Email alert

## 📈 Outcome

Successfully automated detection and stopping of idle EC2 instances

Reduced unnecessary cloud compute costs

Implemented a real-world serverless cost optimization solution

## 🔮 Future Enhancements

Tag-based protection for production instances

Cost savings calculation

Automatic restart during business hours

Multi-account support

## 🏁 Conclusion

This project demonstrates how AWS serverless services can be combined to solve real-world cloud cost challenges efficiently, securely, and at scale.

## 🧑‍💻 Author

Your Name
🔗 GitHub: your-github-link
🔗 LinkedIn: your-linkedin-link
