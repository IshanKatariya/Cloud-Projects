## 🌦️ SkyCast – Serverless Weather Web App (AWS Lambda + SNS)
A fully serverless, cloud-native weather web application that displays real-time weather information through a browser-based UI, fetches live data from a public weather API, and sends automated weather reports via Amazon SNS — built using AWS Free Tier services.

## 🚀 Project Overview
Checking weather is a common daily requirement, but most applications rely on traditional servers.  
SkyCast demonstrates how a **modern, serverless web application** can be built using AWS services without managing any infrastructure.

This project:
- Serves an HTML web page directly from AWS Lambda
- Fetches real-time weather data using an external API
- Sends automated weather reports via email using Amazon SNS
- Uses API Gateway as the HTTP interface
- Runs fully serverless with zero server management

## 🛠️ Tech Stack
- AWS Lambda (Python) – Backend logic + HTML rendering
- Amazon API Gateway (HTTP API) – Web endpoint & routing
- Amazon SNS – Weather report notifications (Email/SMS)
- OpenWeather API – Real-time weather data
- HTML, CSS, JavaScript – Frontend UI
- Amazon CloudWatch Logs – Monitoring & debugging

✅ 100% Serverless  
✅ AWS Free Tier compatible  
❌ No EC2  
❌ No Containers  
❌ No Databases  

## 🎯 Project Use Case
SkyCast can be used for:
- 🌍 Real-time weather lookup from any browser
- 📩 Automated weather email alerts
- 🎓 Learning serverless web architecture
- 💼 Cloud & DevOps portfolio projects
- 🚀 Hackathons and academic demonstrations

## 🧠 How It Works
1. User opens the API Gateway base URL in a browser
2. AWS Lambda returns an HTML weather web page
3. User enters a city name and clicks Search
4. JavaScript calls the `/weather` API endpoint
5. Lambda fetches real-time data from OpenWeather API
6. Weather data is returned to the webpage
7. Lambda publishes a weather report to Amazon SNS
8. User receives the report via email/SMS

## 🏗️ Architecture

<img width="770" height="340" alt="Cloud Project (weather api ) architecture" src="https://github.com/user-attachments/assets/5006f73c-a37a-4b07-8856-2a0a499ef887" />

Flow:

User Browser  
↓  
Amazon API Gateway (HTTP API)  
↓  
AWS Lambda  
↓  
OpenWeather API (Weather Data)  
↓  
Amazon SNS (Email Notification)

## 📦 Setup & Implementation

## 1️⃣ Create SNS Topic
- Create a Standard SNS topic
- Add an Email subscription
- Confirm the subscription from your inbox

![WhatsApp Image 2025-12-31 at 2 36 17 PM](https://github.com/user-attachments/assets/502fd730-3933-4463-82c9-885cd0487e09)


## 2️⃣ Create IAM Role for Lambda
Permissions:
- AmazonSNSFullAccess
- CloudWatchLogsFullAccess


## 3️⃣ Create Lambda Function
- Runtime: Python 3.10
- Handler: index.lambda_handler
- Timeout: 10 seconds
- Execution Role: Custom IAM role

![WhatsApp Image 2025-12-31 at 4 07 46 PM](https://github.com/user-attachments/assets/1f61efd2-0818-4ee3-b614-3b682c49c489)


Lambda responsibilities:
- Serve HTML page at `/`
- Handle weather API requests at `/weather`
- Publish weather report to SNS

## 4️⃣ API Gateway Configuration
- API Type: HTTP API
- Routes:
  - GET `/` → Lambda (HTML UI)
  - GET `/weather` → Lambda (JSON response)
- Enable CORS (Allow all origins)
- Deploy API

## 5️⃣ Frontend (Embedded HTML)
- HTML, CSS, and JavaScript are embedded directly inside Lambda
- Browser renders the UI when API Gateway base URL is opened
- Fetch API is used to retrieve live weather data

## 🧪 Testing
1. Open the API Gateway base URL in browser  
   → HTML page loads
2. Enter a city name and click Search  
   → Weather details appear on screen
    ![WhatsApp Image 2025-12-31 at 4 08 35 PM](https://github.com/user-attachments/assets/7ffcefb4-41cc-466b-ba97-793a38d4f03e)

3. Check email inbox  
   → SNS weather report received
    ![WhatsApp Image 2025-12-31 at 4 08 35 PM](https://github.com/user-attachments/assets/96841ade-c3e8-44a2-87bc-3da50b03fd4e)

## ⚠️ Limitations
- Depends on external weather API availability
- Requires active SNS email subscription
- Basic UI (can be enhanced further)

## 🔮 Future Enhancements
- Add DynamoDB to store search history
- Add forecast (next 5 days)
- Deploy frontend separately using S3 static hosting
- Add user-specific subscriptions
- Improve UI with icons & animations

## 🧾 Resume Bullet
Built a fully serverless weather web application using AWS Lambda and API Gateway to render an HTML frontend, fetch real-time weather data from a public API, and send automated weather reports via Amazon SNS.

## 🧑‍💻 Author
Aarya Agrawal  

GitHub: [Aarya Agrawal]()  
LinkedIn: [Aarya Agrawal](https://www.linkedin.com/in/aaryaagrawal65/)
