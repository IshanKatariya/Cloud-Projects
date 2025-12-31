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

4️⃣ Lambda Logic

Key features:

Reads PDFs from S3

Uses BytesIO for safe PDF parsing

Cleans extracted text

Applies lightweight NLP summarization

Saves summary back to S3

5️⃣ API Gateway

HTTP API

POST endpoint to trigger Lambda

Used for testing and future UI integration

## 🧪 Testing

Upload a text-based PDF to S3

Trigger Lambda via test event or API

Verify:

Lambda returns status 200

Summary file appears in S3

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

GitHub: add your link

LinkedIn: add your link
