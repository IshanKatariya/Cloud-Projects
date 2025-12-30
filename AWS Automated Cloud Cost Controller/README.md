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

<img width="1040" height="360" alt="Cloud Project 1 architecture" src="https://github.com/user-attachments/assets/fc4cca4f-bce9-470b-97b0-0030acb2e827" />


<img width="902" height="624" alt="image" src="https://github.com/user-attachments/assets/a9ba9e99-6056-4aca-ba5a-cfefb8d89e53" />



## 📦 Setup Guide
## 🔹 1. Create an EC2 Test Instance

Launch an EC2 instance using Amazon Linux

Keep the instance idle (no workload)

<img width="1919" height="927" alt="Screenshot 2025-12-31 013129" src="https://github.com/user-attachments/assets/1807b5de-30cb-4539-be8f-37ecf2091cbd" />


## 🔹 2. Create SNS Topic

Go to Amazon SNS → Create topic

Choose Standard

Name: ec2-idle-alerts

<img width="1910" height="925" alt="Screenshot 2025-12-31 013425" src="https://github.com/user-attachments/assets/bd661f1d-1556-4988-bfdd-3fd9138d040b" />


## 🔹 3. Subscribe Email to SNS

Open the SNS topic

Create subscription

Protocol: Email

Endpoint: your email

Confirm subscription from inbox

<img width="1919" height="610" alt="image" src="https://github.com/user-attachments/assets/f471bb78-9845-4215-9184-8903c5e74da3" />


## 🔹 4. Create IAM Role for Lambda

Attach the following permissions:

AmazonEC2FullAccess

CloudWatchReadOnlyAccess

AmazonSNSFullAccess

<img width="1516" height="364" alt="Screenshot 2025-12-31 013718" src="https://github.com/user-attachments/assets/da4b2766-7d20-4dd9-9c55-96f322f5a1ca" />


## 🔹 5. Create Lambda Function

Runtime: Python

Attach the IAM role

Add logic to:

Read CPU metrics

Stop idle EC2 instances

Send SNS email

<img width="1917" height="922" alt="Screenshot 2025-12-31 013814" src="https://github.com/user-attachments/assets/828ef8c9-c895-4e30-8144-769503968466" />
<img width="1918" height="916" alt="Screenshot 2025-12-31 014348" src="https://github.com/user-attachments/assets/cff52a34-e41e-4514-8f45-ae45fc570f7f" />


## 🔹 6. Create Scheduled Rule (EventBridge)

Create a rule using Visual Rule Builder

Schedule expression:

rate(30 minutes)


Target: Lambda function

<img width="1883" height="893" alt="Screenshot 2025-12-31 014859" src="https://github.com/user-attachments/assets/91acfab7-09da-49df-919b-83dde33408f0" />
<img width="1775" height="595" alt="Screenshot 2025-12-31 014955" src="https://github.com/user-attachments/assets/0a54dc36-a9b9-42cd-ab8c-b0039b872406" />


## ✅ Testing the System

Keep EC2 instance idle

Wait for EventBridge to trigger Lambda

EC2 state changes from Running → Stopped

Verify:

Lambda logs (CloudWatch)

SNS email notification

<img width="1916" height="924" alt="Screenshot 2025-12-31 015328" src="https://github.com/user-attachments/assets/f23bb84c-1db6-4adf-9d7b-d9f4eb8e90fe" />
<img width="1917" height="918" alt="Screenshot 2025-12-31 015349" src="https://github.com/user-attachments/assets/f45896aa-aefc-47f0-8cdf-7ad70ce99d66" />


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




