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

![WhatsApp Image 2026-01-02 at 4 38 51 PM](https://github.com/user-attachments/assets/da7c1953-cf67-4a06-bb1d-b95972dfb09f)


## 2️⃣ Create Lambda Function

Runtime: Python 3.x

Handler: index.lambda_handler

Paste the project code into index.py

![WhatsApp Image 2026-01-02 at 4 37 56 PM](https://github.com/user-attachments/assets/30bbe148-cc6e-48b4-82e9-b14d9ec3b8db)


## 3️⃣ Configure API Gateway

Create an HTTP API with routes:

Method	Path	Integration
GET	/	Lambda
POST	/	Lambda
OPTIONS	/	Lambda

Enable CORS.

![WhatsApp Image 2026-01-02 at 4 38 06 PM](https://github.com/user-attachments/assets/310e475b-de3d-4334-a10a-7532fa873b28)


## 4️⃣ Deploy & Test

Open API invoke URL in browser

Start chatting 🎉

![WhatsApp Image 2026-01-02 at 6 45 22 PM](https://github.com/user-attachments/assets/a1047f9c-e7d0-4748-bbfc-5c124067ac3e)


## ✍🏼 Python Code

    import json
    import boto3
    from datetime import datetime
    
    # DynamoDB
    dynamodb = boto3.resource("dynamodb")
    table = dynamodb.Table("ChatbotMessages")
    
    HTML_PAGE = """
    <!DOCTYPE html>
    <html lang="en">
    <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Advanced AI Chatbot</title>
    
    <style>
    :root {
        --bg: #0f172a;
        --card: rgba(255,255,255,0.08);
        --border: rgba(255,255,255,0.15);
        --user: #2563eb;
        --bot: #1e293b;
        --text: #e5e7eb;
        --muted: #94a3b8;
    }
    * { box-sizing: border-box; }
    body {
        margin: 0;
        height: 100vh;
        background: radial-gradient(circle at top, #1e293b, #020617);
        font-family: system-ui, sans-serif;
        display: flex;
        align-items: center;
        justify-content: center;
        color: var(--text);
    }
    .chat-container {
        width: 100%;
        max-width: 420px;
        height: 85vh;
        background: var(--card);
        border: 1px solid var(--border);
        border-radius: 16px;
        display: flex;
        flex-direction: column;
        overflow: hidden;
    }
    .chat-header {
        padding: 16px;
        border-bottom: 1px solid var(--border);
        text-align: center;
        font-weight: 600;
    }
    .chat-messages {
        flex: 1;
        padding: 16px;
        overflow-y: auto;
    }
    .message {
        max-width: 80%;
        padding: 12px;
        margin-bottom: 10px;
        border-radius: 14px;
        font-size: 14px;
    }
    .user {
        background: var(--user);
        margin-left: auto;
    }
    .bot {
        background: var(--bot);
    }
    .typing {
        font-size: 13px;
        color: var(--muted);
    }
    .chat-input {
        display: flex;
        padding: 12px;
        border-top: 1px solid var(--border);
        gap: 10px;
    }
    .chat-input input {
        flex: 1;
        padding: 12px;
        border-radius: 12px;
        border: 1px solid var(--border);
        background: rgba(255,255,255,0.05);
        color: white;
    }
    .chat-input button {
        padding: 0 18px;
        border-radius: 12px;
        border: none;
        background: #2563eb;
        color: white;
        cursor: pointer;
    }
    </style>
    </head>
    
    <body>
    <div class="chat-container">
        <div class="chat-header">🤖 Advanced AI Assistant</div>
        <div class="chat-messages" id="messages"></div>
        <div class="chat-input">
            <input id="text" placeholder="Ask me anything..." />
            <button onclick="send()">Send</button>
        </div>
    </div>
    
    <script>
    const API_URL = window.location.href;
    const messages = document.getElementById("messages");
    const input = document.getElementById("text");
    let sending = false;
    
    function addMessage(text, type) {
        const div = document.createElement("div");
        div.className = "message " + type;
        div.textContent = text;
        messages.appendChild(div);
        messages.scrollTop = messages.scrollHeight;
    }
    
    function send() {
        if (sending) return;
        const text = input.value.trim();
        if (!text) return;
    
        sending = true;
        addMessage(text, "user");
        input.value = "";
    
        const typing = document.createElement("div");
        typing.className = "typing";
        typing.id = "typing";
        typing.textContent = "AI is typing...";
        messages.appendChild(typing);
    
        fetch(API_URL, {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify({ sessionId: "user1", message: text })
        })
        .then(res => res.text())
        .then(raw => {
            document.getElementById("typing").remove();
            try {
                const data = JSON.parse(raw);
                addMessage(data.reply || "No response", "bot");
            } catch {
                addMessage("Invalid server response", "bot");
            }
            sending = false;
        })
        .catch(() => {
            document.getElementById("typing").remove();
            addMessage("Error connecting to server.", "bot");
            sending = false;
        });
    }
    
    input.addEventListener("keydown", e => {
        if (e.key === "Enter") send();
    });
    </script>
    </body>
    </html>
    """

    def get_ai_reply(message):
        msg = message.lower().strip()

        # Greetings
        if any(word in msg for word in ["hello", "hi", "hey"]):
            return "Hello! 😊 How can I assist you today?"
    
        if "how are you" in msg:
            return "I'm doing well, thank you for asking! How can I help you?"
    
        # Identity
        if "who are you" in msg:
            return "I am an AI assistant designed to answer questions and assist users with information and guidance."
    
        if "what can you do" in msg:
            return (
                "I can answer general knowledge questions, explain concepts, "
                "help with learning topics, and assist with everyday queries."
            )
    
        # General knowledge
        if "what is ai" in msg or "artificial intelligence" in msg:
            return (
                "Artificial Intelligence refers to machines that can perform tasks "
                "that normally require human intelligence, such as learning, reasoning, and problem-solving."
            )
    
        if "what is machine learning" in msg:
            return (
                "Machine learning is a subset of AI that enables systems to learn from data "
                "and improve performance without being explicitly programmed."
            )
    
        if "what is programming" in msg:
            return (
                "Programming is the process of writing instructions that a computer can execute "
                "to perform specific tasks or solve problems."
            )
    
        # Career & learning
        if "career" in msg:
            return (
                "Choosing a career involves understanding your interests, strengths, and long-term goals. "
                "Continuous learning and adaptability are key to long-term success."
            )
    
        if "how to learn coding" in msg:
            return (
                "Start with a beginner-friendly language like Python, practice regularly, "
                "build small projects, and gradually explore advanced topics."
            )
    
        # Motivation & life
        if "motivate" in msg or "motivation" in msg:
            return (
                "Motivation grows when you set clear goals, take small consistent steps, "
                "and remind yourself why you started."
            )
    
        if "success" in msg:
            return (
                "Success is achieved through consistent effort, learning from failures, "
                "and staying committed to your goals."
            )
    
        if "failure" in msg:
            return (
                "Failure is a learning opportunity. Every setback provides insight that helps "
                "you grow stronger and wiser."
            )
    
        # Casual conversation
        if "thank you" in msg or "thanks" in msg:
            return "You're welcome! 😊 I'm happy to help."
    
        if "bye" in msg or "goodbye" in msg:
            return "Goodbye! 👋 Have a great day ahead."
    
        # Default professional fallback
        return (
            "That's an interesting question. I'm still learning and improving, "
            "but I'll do my best to help you with general topics and information."
        )


    def lambda_handler(event, context):
        method = event.get("requestContext", {}).get("http", {}).get("method")

        # CORS
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
    
        # Serve HTML
        if method == "GET":
            return {
                "statusCode": 200,
                "headers": {
                    "Content-Type": "text/html",
                    "Access-Control-Allow-Origin": "*"
                },
                "body": HTML_PAGE
            }
    
        # Chat API
        body = json.loads(event.get("body", "{}"))
        session_id = body.get("sessionId", "default")
        message = body.get("message", "")
    
        reply = get_ai_reply(message)
    
        table.put_item(
            Item={
                "userId": session_id,
                "timestamp": datetime.utcnow().isoformat(),
                "userMessage": message,
                "botReply": reply
            }
        )
    
        return {
            "statusCode": 200,
            "headers": {
                "Content-Type": "application/json",
                "Access-Control-Allow-Origin": "*",
                "Access-Control-Allow-Methods": "GET,POST,OPTIONS",
                "Access-Control-Allow-Headers": "Content-Type"
            },
            "body": json.dumps({"reply": reply})
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

Ishaan Katariya

GitHub: [IshaanKatariya](https://github.com/IshanKatariya)

LinkedIn: [IshaanKatariya](https://www.linkedin.com/in/ishaan-katariya-268b8534a/)
