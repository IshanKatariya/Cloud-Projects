## 📄 AI Document Summarizer for PDFs 

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

**LAMBDA CODE:**

    import base64
    import json
    import re
    from io import BytesIO
    from PyPDF2 import PdfReader
    from collections import Counter

    # -----------------------------
    # HTML PAGE (UPLOAD UI)
    # -----------------------------

    HTML_PAGE = """
    <!DOCTYPE html>
    <html lang="en">
    <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI PDF Summarizer</title>
    
    <style>
    :root {
        --bg: #0f172a;
        --card: #111827;
        --border: #1f2933;
        --primary: #2563eb;
        --primary-hover: #1d4ed8;
        --text: #e5e7eb;
        --muted: #9ca3af;
    }
    
    * {
        box-sizing: border-box;
    }
    
    body {
        margin: 0;
        min-height: 100vh;
        background: radial-gradient(circle at top, #1e293b, #020617);
        font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
        display: flex;
        align-items: center;
        justify-content: center;
        color: var(--text);
    }
    
    .card {
        width: 100%;
        max-width: 420px;
        background: var(--card);
        border: 1px solid var(--border);
        border-radius: 18px;
        padding: 28px;
        box-shadow: 0 20px 40px rgba(0,0,0,0.4);
    }
    
    .header {
        text-align: center;
        margin-bottom: 22px;
    }
    
    .header h1 {
        font-size: 22px;
        margin: 0;
        font-weight: 600;
    }
    
    .header p {
        font-size: 14px;
        color: var(--muted);
        margin-top: 6px;
    }
    
    .upload-box {
        border: 2px dashed var(--border);
        border-radius: 14px;
        padding: 22px;
        text-align: center;
        transition: border-color 0.2s;
    }
    
    .upload-box:hover {
        border-color: var(--primary);
    }
    
    .upload-box input {
        display: none;
    }
    
    .upload-label {
        display: block;
        cursor: pointer;
    }
    
    .upload-label span {
        display: block;
        font-size: 14px;
        color: var(--muted);
        margin-top: 6px;
    }
    
    button {
        width: 100%;
        margin-top: 20px;
        padding: 12px;
        font-size: 15px;
        font-weight: 600;
        border-radius: 12px;
        border: none;
        background: var(--primary);
        color: white;
        cursor: pointer;
        transition: background 0.2s, transform 0.1s;
    }
    
    button:hover {
        background: var(--primary-hover);
    }
    
    button:active {
        transform: scale(0.98);
    }
    
    .footer {
        text-align: center;
        margin-top: 18px;
        font-size: 12px;
        color: var(--muted);
    }
    </style>
    </head>
    
    <body>
    
    <div class="card">
        <div class="header">
            <h1>AI PDF Summarizer</h1>
            <p>Upload a PDF and get a clean summary instantly</p>
        </div>

    <form method="post" enctype="multipart/form-data">
        <div class="upload-box">
            <label class="upload-label">
                <strong>Select PDF File</strong>
                <span>Only .pdf files are supported</span>
                <input type="file" name="file" accept=".pdf" required>
            </label>
        </div>

        <button type="submit">Generate Summary</button>
    </form>

    <div class="footer">
        Powered by AWS Lambda & API Gateway
    </div>
    </div>
    
    </body>
    </html>
    """


    # -----------------------------
    # CLEAN TEXT
    # -----------------------------
    def clean_text(text):
        text = re.sub(r"-\s+", "", text)
        text = re.sub(r"\s+", " ", text)
        return text.strip()
    
    # -----------------------------
    # SUMMARIZATION
    # -----------------------------
    def summarize_text(text, sentence_count=10):
        sentences = re.split(r"(?<=[.!?])\s+", text)

        words = re.findall(r"\w+", text.lower())
        freq = Counter(words)
    
        scores = {}
        for s in sentences:
            for w in re.findall(r"\w+", s.lower()):
                scores[s] = scores.get(s, 0) + freq[w]
    
        return sorted(scores, key=scores.get, reverse=True)[:sentence_count]

    # -----------------------------
    # CREATE SIMPLE PDF (HTML STYLE)
    # -----------------------------
    def create_pdf(sentences):
        html = "<html><body style='font-family:Calibri; font-size:12pt;'>"
        for i in range(0, len(sentences), 3):
            html += f"<p>{' '.join(sentences[i:i+3])}</p>"
        html += "</body></html>"
        return html.encode("utf-8")
    
    # -----------------------------
    # LAMBDA HANDLER
    # -----------------------------
    def lambda_handler(event, context):

        method = event.get("requestContext", {}).get("http", {}).get("method")
    
        # ---------- CORS ----------
        if method == "OPTIONS":
            return {
                "statusCode": 200,
                "headers": {
                    "Access-Control-Allow-Origin": "*",
                    "Access-Control-Allow-Methods": "GET,POST,OPTIONS",
                    "Access-Control-Allow-Headers": "Content-Type"
                },
                "body": ""
            }
    
        # ---------- SERVE WEBSITE ----------
        if method == "GET":
            return {
                "statusCode": 200,
                "headers": {
                    "Content-Type": "text/html",
                    "Access-Control-Allow-Origin": "*"
                },
                "body": HTML_PAGE
            }
    
        # ---------- HANDLE PDF UPLOAD ----------
        if method == "POST":
    
            body = base64.b64decode(event["body"])
    
            reader = PdfReader(BytesIO(body))
            text = ""
    
            for page in reader.pages:
                if page.extract_text():
                    text += page.extract_text() + " "
    
            cleaned = clean_text(text)
            summary_sentences = summarize_text(cleaned)
            pdf_content = create_pdf(summary_sentences)
    
            return {
                "statusCode": 200,
                "headers": {
                    "Content-Type": "text/html",
                    "Content-Disposition": "attachment; filename=summary.html",
                    "Access-Control-Allow-Origin": "*"
                },
                "body": pdf_content.decode("utf-8")
            }

5️⃣ API Gateway

HTTP API

POST endpoint to trigger Lambda

Used for testing and future UI integration

![WhatsApp Image 2026-01-07 at 5 18 34 PM](https://github.com/user-attachments/assets/9afe680d-8e46-47cf-86b8-049d6b5aaefd)


## 🧪 Testing

Upload a text-based PDF to S3

Trigger Lambda via test event or API

Verify:

![WhatsApp Image 2026-01-07 at 5 17 31 PM](https://github.com/user-attachments/assets/92486eef-99b7-4517-87c3-022c527763df)
![WhatsApp Image 2026-01-07 at 5 17 47 PM](https://github.com/user-attachments/assets/bb4428b5-06cb-49b3-b892-6ae032bfd03d)




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

GitHub: [AaryaAgrawal](https://github.com/Aaryagrawal)

LinkedIn: [AaryaAgrawal](https://www.linkedin.com/in/aaryaagrawal65/)



