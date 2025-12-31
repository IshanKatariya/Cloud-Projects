## 📄 AI Document Summarizer for PDFs (AWS + NLP)

A serverless AI-powered application that automatically extracts text from PDF documents, cleans formatting artifacts, generates concise summaries using NLP techniques, and stores the summarized output back to Amazon S3 — built entirely on AWS Free Tier services.

## 🚀 Project Overview

Long documents such as lecture notes, reports, and technical PDFs are time-consuming to read.
This project solves that problem by:

Automatically extracting text from PDFs

Cleaning noisy PDF formatting issues

Applying NLP-based summarization

Saving a readable summary back to cloud storage

The entire system is serverless, scalable, and cost-efficient.

## 🛠️ Tech Stack

AWS Lambda (Python) – Core processing & NLP logic

Amazon S3 – PDF storage and summary output

Amazon API Gateway (HTTP API) – Invocation layer

Amazon CloudWatch Logs – Logging & debugging

Python NLP (Custom lightweight summarizer)

✅ 100% AWS Free Tier compatible
❌ No EC2
❌ No DynamoDB
❌ No paid AI APIs

## 🎯 Project Use Case

This system can be used for:

📚 Students summarizing lecture notes

📄 Professionals analyzing long reports

🏢 Teams reviewing migration or strategy documents

🤖 Automating document analysis pipelines

## 🧠 How It Works

A PDF file is uploaded to an Amazon S3 bucket

AWS Lambda retrieves the PDF

Text is extracted using PyPDF2

Formatting artifacts (extra spaces, broken words, hyphens) are cleaned

NLP-based summarization is applied

The generated summary is saved back to S3 as a text file

## 🏗️ Architecture

<img width="551" height="271" alt="Cloud Project ( pdf summarizer ) architecture" src="https://github.com/user-attachments/assets/605264c2-8a19-442c-83f9-9141cb01734d" />


Flow:

User / API
   ↓
Amazon S3 (PDF Upload)
   ↓
AWS Lambda (Text Extraction + NLP Summarization)
   ↓
Amazon S3 (Summary Output)

📦 Setup & Implementation
1️⃣ Create S3 Bucket

Store input PDFs

Block public access

Enable default encryption (SSE-S3)

<img width="1919" height="921" alt="Screenshot 2025-12-31 102958" src="https://github.com/user-attachments/assets/3bc9845d-8c34-4c20-99a6-3c583cd500bd" />


2️⃣ Create IAM Role for Lambda

Permissions:

AmazonS3ReadOnlyAccess

Custom policy for s3:PutObject (summary storage)

CloudWatchLogsFullAccess


3️⃣ Create Lambda Function

Runtime: Python 3.10

Memory: 512 MB

Timeout: 30 seconds

Execution role: Custom IAM role

<img width="1919" height="922" alt="Screenshot 2025-12-31 103234" src="https://github.com/user-attachments/assets/1d7fdb77-de3e-424f-abf4-14a1b0068330" />

4️⃣ Lambda Logic

Key features:

Reads PDFs from S3

Uses BytesIO for safe PDF parsing

Cleans extracted text

Applies lightweight NLP summarization

Saves summary back to S3

**LAMBDA CODE:**

<img width="1905" height="907" alt="Screenshot 2025-12-31 105345" src="https://github.com/user-attachments/assets/6fefcc74-e1bd-4c6d-851c-fe9f156ce01c" />


5️⃣ API Gateway

HTTP API

POST endpoint to trigger Lambda

Used for testing and future UI integration

## 🧪 Testing

Upload a text-based PDF to S3

Trigger Lambda via test event or API

Verify:

**Lambda returns status 200**

<img width="1919" height="926" alt="Screenshot 2025-12-31 113314" src="https://github.com/user-attachments/assets/b6659d20-e1ce-45f3-8d4a-aa1b9ebe15bd" />



**Summary file appears in S3**
<img width="1919" height="921" alt="Screenshot 2025-12-31 113411" src="https://github.com/user-attachments/assets/39aaa0b2-30b7-418a-afd8-6b0999c7e201" />



<img width="1919" height="777" alt="Screenshot 2025-12-31 114355" src="https://github.com/user-attachments/assets/211264ff-7ad7-4d14-bacb-313e1c211470" />



original_file.pdf
original_file_summary.txt



## ⚠️ Limitations

Supports text-based PDFs only

Scanned or handwritten PDFs require OCR (future enhancement)

## 🔮 Future Enhancements

OCR support using Amazon Textract

Auto-trigger Lambda on S3 upload

Save summaries as Markdown (.md)

Web UI for file upload and summary preview

## 🧾 Resume Bullet

Built a serverless AI-powered PDF document summarizer using AWS Lambda and NLP techniques to extract, clean, and summarize large documents, with automated storage of results in Amazon S3.

## 🧑‍💻 Author

Ishaan Katariya

GitHub: [IshaanKatariya](https://github.com/IshanKatariya)

LinkedIn: [IshaanKatariya](https://www.linkedin.com/in/ishaan-katariya-268b8534a/)


