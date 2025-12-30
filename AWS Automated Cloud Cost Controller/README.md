🌤️ AWS Serverless Weather Alert System
A fully automated serverless project that fetches real-time weather data for a city using OpenWeatherMap API and sends alerts via Amazon SNS when certain conditions are met — all powered by AWS Lambda, EventBridge, and IAM.

🛠️ Tech Stack
AWS Lambda
Amazon SNS
Amazon EventBridge (CloudWatch Events)
OpenWeatherMap API
IAM Roles/Policies
Serverless Architecture
📌 Project Use Case
Many times we want alerts when it's going to rain heavily, storm, or be extremely hot/cold. This project lets you:

✅ Receive automated email alerts based on weather
✅ Run a Lambda function on a schedule (hourly, daily etc.)
✅ Integrate external APIs with AWS

🧠 How It Works
User specifies city → Lambda fetches weather via OpenWeatherMap API
→ If condition (e.g. Rain, Thunderstorm) is met → SNS triggers Email
→ Done!
📐 Architecture Diagram
ChatGPT Image Aug 7, 2025, 01_02_39 PM
+-------------------+       HTTP Request      +-----------------------+
|   EventBridge     |  -------------------->  |    AWS Lambda         |
| (Scheduled Rule)  |                         | (Python weather fetch)|
+-------------------+                         +-----------+-----------+
                                                          |
                                                          | SNS Publish
                                                          ▼
                                                +------------------+
                                                |  Amazon SNS      |
                                                |  (WeatherAlert)  |
                                                +------------------+
                                                         |
                                                Email Alert Sent!
📦 Setup Guide
🔹 1. Create SNS Topic
Go to Amazon SNS → Create topic
Choose Standard
Name: WeatherAlert
Click Create Topic
📸 Screenshot 2025-07-18 171121 Screenshot 2025-07-18 171137

🔹 2. Subscribe an Email to SNS
Inside your topic → Click Create subscription
Protocol: Email
Endpoint: Your email address
Confirm subscription from your inbox.
📸 Screenshot 2025-07-18 171228

🔹 3. Get API Key from OpenWeatherMap
Go to: https://openweathermap.org/api
Sign up → Copy the API Key
📸 Screenshot 2025-08-07 120501

🔹 4. Create Lambda Function
Runtime: Python 3.12
Name: weatheralertfunction
Paste the following code:
import json
import urllib.request
import boto3

sns = boto3.client("sns")

def lambda_handler(event, context):
    city = "Mumbai"  # You can replace this with your city.
    api_key = "YOUR_OPENWEATHERMAP_API_KEY"
    url = f"http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric"

    try:
        with urllib.request.urlopen(url) as response:
            data = json.loads(response.read().decode("utf-8"))

        temperature = data["main"]["temp"]
        weather = data["weather"][0]["description"]

        message = f"🌦️ Weather Alert for {city}:\nTemperature: {temperature}°C\nCondition: {weather}"

        if "rain" in weather.lower() or temperature > 40:
            message += "\n⚠️ Warning: Extreme conditions!"

        # Replace with your actual SNS Topic ARN
        sns.publish(
            TopicArn="YOUR_SNS_TOPIC_ARN",
            Message=message,
            Subject="🚨 Weather Alert"
        )

        return {
            "statusCode": 200,
            "body": json.dumps({"message": "Alert sent successfully", "details": message})
        }

    except Exception as e:
        return {
            "statusCode": 500,
            "body": json.dumps({"error": str(e)})
        }
📸 Screenshot 2025-07-18 170524 Screenshot 2025-07-18 170710

🔹 5. Add IAM Permissions to Lambda and Edit Environment Variables.
Go to Lambda → Permissions tab
Click on Execution Role
Attach Policy: In JSON or VISUAL
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "sns:Publish",
      "Resource": "arn:aws:sns:us-east-1:YOUR_ACCOUNT_ID:WeatherAlert"
    }
  ]
}
📸 Screenshot 2025-07-18 171522 Screenshot 2025-07-18 171636 Screenshot 2025-07-18 172725 Screenshot 2025-07-18 172735 Screenshot 2025-07-18 173039 Screenshot 2025-07-18 173200

🔹 6. Create Scheduled Trigger (EventBridge)
Go to Lambda → Triggers → + Add trigger
Choose: EventBridge (CloudWatch Events)
Create a new rule:
Name: HourlyWeatherCheck
Schedule expression: rate(1 hour)
Save trigger.
📸 Screenshot 2025-07-18 173329 Screenshot 2025-07-18 173606

✅ Testing the System
Click Test inside Lambda to trigger manually.
Or wait for EventBridge to invoke it on schedule.
Check your inbox for email like:
Subject: ⚠️ Weather Alert
Body: Weather Alert for Pune: Thunderstorm, Temperature: 31°C
📸 Screenshot 2025-07-18 173816

🏁 Conclusion
This project gave me hands-on experience with:

Real-world API integration
AWS SNS notifications
Scheduled event triggers
IAM roles & permissions
🧑‍💻 Author
UJJWAL WADHAI

🔗 GitHub 🔗 LinkedIn

