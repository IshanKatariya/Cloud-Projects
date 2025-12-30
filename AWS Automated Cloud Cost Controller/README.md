💰 AWS Automated Cloud Cost Controller

A fully automated cloud cost optimization project that identifies idle Amazon EC2 instances using CloudWatch metrics and automatically stops them to avoid unnecessary AWS charges — all powered by AWS Lambda, Amazon EventBridge, Amazon SNS, and IAM.

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
