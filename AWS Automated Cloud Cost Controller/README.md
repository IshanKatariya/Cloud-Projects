💰 AWS Automated Cloud Cost Controller

A fully automated cloud cost optimization project that detects idle Amazon EC2 instances using CloudWatch metrics and automatically stops them to avoid unnecessary AWS charges. The solution is built using a serverless architecture powered by AWS Lambda, Amazon EventBridge, Amazon SNS, and IAM.

🛠️ Tech Stack

AWS EC2
AWS Lambda (Python)
Amazon CloudWatch
Amazon EventBridge (Scheduler)
Amazon SNS
IAM Roles & Policies
Serverless Architecture

📌 Project Use Case

In many cloud environments, EC2 instances are left running even when they are not actively used. This leads to unnecessary cloud expenses. This project helps to automatically identify such idle instances and stop them without manual intervention.

Key benefits:
• Automatically stops idle EC2 instances
• Reduces AWS cloud costs
• Eliminates manual monitoring
• Sends email notifications when an action is taken

🧠 How It Works

EventBridge triggers the Lambda function on a fixed schedule.
Lambda retrieves CPU utilization metrics for running EC2 instances from CloudWatch.
If the CPU utilization is below a defined threshold, the EC2 instance is considered idle.
The idle EC2 instance is stopped automatically.
An email notification is sent using Amazon SNS.

📐 Architecture Overview

EventBridge (Scheduled Rule) triggers AWS Lambda.
AWS Lambda queries CloudWatch for EC2 CPU utilization metrics.
Based on the metrics, Lambda stops idle EC2 instances.
Amazon SNS sends an email alert to notify the user of the action taken.

📦 Setup Guide

Step 1: Create an EC2 test instance
Launch an EC2 instance using Amazon Linux and keep it idle without any workload.

Step 2: Create an SNS topic
Create an Amazon SNS topic and configure an email subscription. Confirm the subscription from your email.

Step 3: Create an IAM role for Lambda
Create an IAM role with permissions to access EC2, CloudWatch, and SNS services.

Step 4: Create the Lambda function
Create a Lambda function using Python runtime and attach the IAM role. Add logic to check EC2 CPU utilization and stop idle instances.

Step 5: Create a scheduled rule using EventBridge
Configure an EventBridge rule with a rate-based schedule to invoke the Lambda function automatically.

✅ Testing and Validation

Keep the EC2 instance idle.
Wait for the EventBridge rule to trigger the Lambda function.
Verify that the EC2 instance state changes from running to stopped.
Check CloudWatch logs for Lambda execution details.
Confirm receipt of SNS email notification.

📈 Outcome

The project successfully reduced unnecessary EC2 runtime by automatically stopping idle instances. It demonstrated real-world cloud cost optimization using serverless AWS services.

🔮 Future Enhancements

Add tag-based protection for production instances.
Calculate and display cost savings.
Automatically restart instances during business hours.
Extend the solution to support multiple AWS accounts.

🏁 Conclusion

This project provided hands-on experience with AWS automation, serverless architecture, cloud monitoring, and cost optimization. It demonstrates how cloud-native services can be combined to solve real operational problems efficiently.

🧑‍💻 Author

Your Name
GitHub: your-github-link
LinkedIn: your-linkedin-link
