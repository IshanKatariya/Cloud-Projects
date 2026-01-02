## 🤖 Serverless AI Chatbot (AWS)

A fully serverless chatbot application built using AWS Lambda, API Gateway, and DynamoDB, capable of answering general user questions through a responsive web interface.
The chatbot serves its frontend directly from AWS Lambda and provides consistent, professional responses without relying on paid AI services.

## 🚀 Project Overview

This project demonstrates how to build a serverless conversational chatbot that:

Serves a complete HTML + CSS + JavaScript UI from AWS Lambda

Handles real-time chat requests via API Gateway

Stores chat history in Amazon DynamoDB

Uses structured intent matching to provide professional responses

Works entirely within AWS Free Tier

Requires no external paid APIs

## 🛠️ Tech Stack

AWS Lambda – Backend logic & HTML rendering

Amazon API Gateway (HTTP API) – Request routing (GET /, POST /)

Amazon DynamoDB – Chat message storage

Python 3.x – Lambda runtime

HTML / CSS / JavaScript – Frontend UI

Serverless Architecture

## 📌 Key Features

🌐 Single API endpoint for UI and chat handling

💬 Real-time chatbot interaction

📦 Persistent chat storage using DynamoDB

⚡ No servers to manage

💰 Completely free-tier compatible

🧠 Professional, deterministic responses

## 🧠 How It Works

1. User opens the API URL in a browser
2. GET / → Lambda returns the chatbot HTML page
3. User submits a message
4. POST / → Lambda processes the message
5. Response is generated using structured intent matching
6. Chat is stored in DynamoDB
7. Reply is sent back to the browser

## 🏗️ Architecture

<img width="701" height="381" alt="Cloud Project ( chatbot) architecture" src="https://github.com/user-attachments/assets/10c369a2-fe88-4318-81a6-14f9c0e3f016" />


User Browser
     |
     v
API Gateway (HTTP API)
     |
     v
AWS Lambda
  ├─ Serve HTML UI (GET)
  ├─ Process chat (POST)
  └─ Store messages
     |
     v
Amazon DynamoDB


## 📦 DynamoDB Table Design

Table Name: ChatbotMessages

Attribute	Type
userId	String (Partition Key)
timestamp	String
userMessage	String
botReply	String


## 🧑‍💻 Setup Instructions
## 1️⃣ Create DynamoDB Table

Table name: ChatbotMessages

Partition key: userId (String)



## 2️⃣ Create Lambda Function

Runtime: Python 3.x

Handler: index.lambda_handler

Paste the project code into index.py

![WhatsApp Image 2026-01-02 at 2 54 04 PM](https://github.com/user-attachments/assets/29861b12-92cf-414d-836d-6af89f9c5223)


## 3️⃣ Configure API Gateway

Create an HTTP API with routes:

Method	Path	Integration
GET	/	Lambda
POST	/	Lambda
OPTIONS	/	Lambda

Enable CORS.

![WhatsApp Image 2026-01-02 at 3 47 37 PM](https://github.com/user-attachments/assets/f87dfe85-0865-49b8-8f38-c647d9cf56bb)


## 4️⃣ Deploy & Test

Open API invoke URL in browser

Start chatting 🎉

![WhatsApp Image 2026-01-02 at 3 57 13 PM](https://github.com/user-attachments/assets/63bdf85f-ecbc-4f74-a2c8-d9cad87c9027)


## ✍🏼 Python Code


    import json
    
    def lambda_handler(event, context):

    <html>
    <head>
        <title>Serverless Cloud Chatbot</title>
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <style>
            * { box-sizing: border-box; font-family: Arial, sans-serif; }

            body {
                margin: 0;
                height: 100vh;
                background: linear-gradient(135deg, #1d2671, #c33764);
                display: flex;
                justify-content: center;
                align-items: center;
            }
    
            .chat-container {
                width: 360px;
                height: 520px;
                background: rgba(255,255,255,0.18);
                backdrop-filter: blur(16px);
                border-radius: 20px;
                display: flex;
                flex-direction: column;
                color: white;
            }
    
            .chat-header {
                padding: 15px;
                text-align: center;
                font-weight: bold;
                border-bottom: 1px solid rgba(255,255,255,0.2);
            }
    
            .chat-body {
                flex: 1;
                padding: 12px;
                overflow-y: auto;
            }
    
            .bubble {
                max-width: 75%;
                padding: 10px 14px;
                border-radius: 14px;
                margin-bottom: 10px;
                font-size: 14px;
            }
    
            .user {
                background: #4facfe;
                margin-left: auto;
                text-align: right;
            }
    
            .bot {
                background: rgba(255,255,255,0.3);
                margin-right: auto;
                text-align: left;
            }
    
            .chat-footer {
                padding: 10px;
                display: flex;
                gap: 8px;
                border-top: 1px solid rgba(255,255,255,0.2);
            }
    
            input {
                flex: 1;
                padding: 10px;
                border-radius: 10px;
                border: none;
            }
    
            button {
                padding: 10px 14px;
                border-radius: 10px;
                border: none;
                background: #4facfe;
                color: white;
            }
        </style>
    </head>
    
    <body>
    
    <div class="chat-container">
        <div class="chat-header">Serverless Cloud Chatbot</div>

        <div class="chat-body" id="chat">
            <div class="bubble bot">
                Hello. Ask me anything — technology, life, studies, or general questions.
            </div>
        </div>
    
        <div class="chat-footer">
            <input id="msg" placeholder="Type your message..." />
            <button onclick="send()">Send</button>
        </div>
    </div>
    
    <script>
    async function send() {
        const input = document.getElementById("msg");
        const chat = document.getElementById("chat");
        const message = input.value.trim();
        if (!message) return;
    
        chat.innerHTML += `<div class="bubble user">${message}</div>`;
        input.value = "";
        chat.scrollTop = chat.scrollHeight;
    
        const res = await fetch(window.location.href, {
            method: "POST",
            headers: {"Content-Type": "application/json"},
            body: JSON.stringify({ message })
        });
    
        const reply = await res.text();
        chat.innerHTML += `<div class="bubble bot">${reply}</div>`;
        chat.scrollTop = chat.scrollHeight;
    }
    </script>
    
    </body>
    </html>"""

        # ---------------- SMART ANY-TOPIC LOGIC ----------------
        if event.get("requestContext", {}).get("http", {}).get("method") == "POST":
            body = json.loads(event.get("body", "{}"))
            msg = body.get("message", "").lower()
    
            # greetings
            if any(w in msg for w in ["hi", "hello", "hey"]):
                reply = "Hello. What would you like to know?"
    
            # common personal
            elif "how are you" in msg:
                reply = "I am functioning as expected. Thanks for asking."
    
            # tech / cloud
            elif any(w in msg for w in ["aws", "cloud", "serverless", "lambda"]):
                reply = (
                    "AWS provides cloud services that help build scalable applications. "
                    "Serverless means you do not manage servers; the cloud handles it."
                )
    
            # study / career
            elif any(w in msg for w in ["career", "job", "study", "exam"]):
                reply = (
                    "Consistency and practical projects are key. "
                    "Focus on fundamentals and apply them in real projects."
                )
    
            # life / philosophy
            elif any(w in msg for w in ["life", "meaning", "purpose"]):
                reply = (
                    "Different people find meaning in different things. "
                    "Learning, growth, and relationships often play a big role."
                )
    
            # question types
            elif msg.startswith("why"):
                reply = (
                    "That is a thoughtful question. "
                    "The answer often depends on context and perspective."
                )
    
            elif msg.startswith("how"):
                reply = (
                    "The process usually involves multiple steps. "
                    "If you want, you can ask about a specific part."
                )
    
            elif msg.startswith("what"):
                reply = (
                    "That topic has many aspects. "
                    "Could you clarify what exactly you want to know?"
                )
    
            # fallback (ANY RANDOM SH*T)
            else:
                reply = (
                    "That is an interesting topic. "
                    "This chatbot provides general guidance, "
                    "but deeper answers would require advanced AI integration."
                )
    
            return {
                "statusCode": 200,
                "headers": {"Content-Type": "text/plain; charset=utf-8"},
                "body": reply
            }
    
        return {
            "statusCode": 200,
            "headers": {"Content-Type": "text/html; charset=utf-8"},
            "body": html
        }

## 🧠 Design Decisions

Rule-based responses ensure reliability and zero cost

Single Lambda endpoint simplifies architecture

Frontend served from Lambda avoids S3/CloudFront complexity

DynamoDB provides scalable, serverless persistence

## 📈 Future Enhancements

Add conversation memory per user

Store responses externally (JSON / DynamoDB knowledge base)

Integrate free or paid AI models optionally

Deploy frontend via S3 + CloudFront

Add authentication (Cognito)


## 👨‍💻 Author

Aarya Agrawal  

GitHub: [Aarya Agrawal](https://github.com/Aaryagrawal)  
LinkedIn: [Aarya Agrawal](https://www.linkedin.com/in/aaryaagrawal65/)
