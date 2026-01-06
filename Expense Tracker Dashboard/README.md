## 💰 Expense Tracker Dashboard (AWS + Power BI)

A cloud-based expense tracking system that stores financial data in AWS RDS (MySQL) and visualizes spending patterns using Power BI dashboards.
This project demonstrates end-to-end data flow from application layer to cloud database and business intelligence reporting.

## 🚀 Project Overview

Managing personal or organizational expenses requires structured storage and clear insights.
This project enables users to:

Store expense data securely in AWS RDS

Query and analyze expenses using SQL

Visualize trends and insights using Power BI

Track spending by category, date, and payment mode

## 🛠️ Tech Stack

Python – Data insertion and database connectivity

AWS RDS (MySQL Community Edition) – Cloud database

Amazon EC2 / Local Machine – Python execution environment

Power BI Desktop – Data visualization and dashboard creation

SQL – Querying and analysis

## 📌 Use Case

Personal finance tracking

Expense analysis for small businesses

Demonstrating cloud database + BI integration

Resume-ready cloud analytics project

## 🧠 How It Works

Expense data is inserted into AWS RDS (MySQL) using Python

Data is stored in a structured expenses table

Power BI connects directly to the RDS database

Dashboards visualize totals, trends, and category-wise spending

## 🏗️ Architecture


<img width="552" height="282" alt="Cloud Project (expense tracker ) architecture" src="https://github.com/user-attachments/assets/f9709173-5028-43c3-87c9-9242d54039ae" />

Client / Python Script → AWS RDS (MySQL) → Power BI Dashboard

Services used:

AWS RDS

MySQL

Power BI

## 🗄️ Database Schema

**Table: expenses**

Column Name	          Type	        Description
id	                 INT (PK)	      Expense ID
date	               DATE	          Expense date
category	           VARCHAR	      Expense category
amount	             DECIMAL	      Amount spent
payment_mode         VARCHAR	      Cash / UPI / Card
description	         VARCHAR	      Expense details


## 🧪 Sample Python Code

    import mysql.connector
    
    conn = mysql.connector.connect(
        host="expense-tracker-db.ckrw8cuqoauu.us-east-1.rds.amazonaws.com",
        user="admin",
        password="ishan0507",
        database="expense_tracker"
    )
    
    cursor = conn.cursor()
    
    query = """
    INSERT INTO expenses (date, category, amount, payment_mode, description)
    VALUES (%s, %s, %s, %s, %s)
    """
    
    data = ("2026-01-02", "Food", 300, "UPI", "Dinner")
    
    cursor.execute(query, data)
    conn.commit()
    
    print("Expense added successfully")
    
    cursor.close()
    conn.close()


## 📸 Dashboard Preview

![WhatsApp Image 2026-01-06 at 8 46 08 PM](https://github.com/user-attachments/assets/bccdc962-4d5c-408d-a901-42c38a706a73)

![WhatsApp Image 2026-01-06 at 8 45 28 PM](https://github.com/user-attachments/assets/ce01af45-68dc-446a-8d0a-351c6e4dced4)
<img width="987" height="567" alt="image" src="https://github.com/user-attachments/assets/f1baf30f-47a9-4688-9ad8-23395e9b4910" />


## ✅ Key Learnings

AWS RDS configuration and connectivity

MySQL database design

Python-to-cloud database integration

Power BI data modeling and visualization

Real-world cloud analytics workflow

## 🔮 Future Enhancements

Web-based expense input form

User authentication

Budget alerts and notifications

Monthly expense forecasting

Power BI service publishing


## 👨‍💻 Author

Ishaan Katariya

GitHub: [IshaanKatariya](https://github.com/IshanKatariya)

LinkedIn: [IshaanKatariya](https://www.linkedin.com/in/ishaan-katariya-268b8534a/)

