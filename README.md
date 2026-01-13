## ☁️ Cloud Data Analytics Pipeline using AWS & Power BI

This project demonstrates a real-world cloud-based data analytics pipeline that automatically ingests, processes, stores, and visualizes business data using AWS and Power BI.

The system uses Amazon S3 for data storage, AWS Glue for ETL, Amazon Redshift as a data warehouse, and Power BI for analytics and reporting.

---

## 🧠 Project Overview

The pipeline automates the flow of sales data from raw CSV files into a structured data warehouse and visualizes business insights in Power BI.

### Data Flow


Whenever a new CSV file is uploaded to S3, the ETL pipeline processes it and updates the analytics dashboard automatically.

---

## 🛠 Technologies Used

| Layer | Technology |
|------|-----------|
| Storage | Amazon S3 |
| Data Catalog | AWS Glue Data Catalog |
| ETL Engine | AWS Glue |
| Data Warehouse | Amazon Redshift Serverless |
| Visualization | Power BI |
| Networking | VPC, S3 VPC Endpoint |
| Security | IAM, Security Groups |

---

## 📂 Dataset

The project uses a sales dataset (`sales.csv`) with the following columns:

- order_id  
- order_date  
- customer_name  
- product  
- category  
- quantity  
- price  
- region  
- payment_method  

---

## 🏗 Architecture

The system follows a **cloud-native data analytics architecture** where data moves through multiple AWS services before being visualized in Power BI.

<img width="650" height="370" alt="Cloud Project ( Pipeline database ) architecture" src="https://github.com/user-attachments/assets/0a4f114b-0f2c-4325-b104-8c3afa4d5351" />


## 📸Screenshots 

<img width="1365" height="427" alt="image" src="https://github.com/user-attachments/assets/d194f503-ef1f-4429-b377-dbb83c37bef4" />
<img width="1365" height="497" alt="image" src="https://github.com/user-attachments/assets/50e242c0-4a3b-47d6-82cb-71876f2c21e8" />
<img width="1365" height="660" alt="image" src="https://github.com/user-attachments/assets/0cb7b564-b3b7-4322-a77a-21efa45cc9e4" />
<img width="1365" height="651" alt="image" src="https://github.com/user-attachments/assets/8c5ddafd-0fc5-4b8b-99cb-a77b7c6796de" />
<img width="1365" height="452" alt="image" src="https://github.com/user-attachments/assets/31a28406-be74-4725-96d8-64e7e7b8d1d7" />

<img width="833" height="291" alt="image" src="https://github.com/user-attachments/assets/f4327d64-d86f-4024-ae38-d77731043c8f" />


## ⚙️ How the Pipeline Works

1. **Data Ingestion**
   - Sales CSV files are uploaded to Amazon S3.
   - The raw data is stored in a secure S3 bucket.

2. **Schema Detection**
   - AWS Glue Crawler scans the S3 bucket and creates table metadata in the Glue Data Catalog.

3. **Data Transformation**
   - AWS Glue Visual ETL job:
     - Reads data from Glue Catalog
     - Converts numeric columns (price, quantity)
     - Cleans data
     - Prepares it for analytics

4. **Data Loading**
   - AWS Glue loads the transformed data into Amazon Redshift Serverless.

5. **Analytics**
   - Power BI connects to Redshift and displays dashboards such as:
     - Total Revenue
     - Sales by Region
     - Product Performance
     - Payment Method Distribution
     - Sales Trend

---

## 📊 Power BI Measures

Revenue is calculated using:

```DAX
Total Revenue = 
SUMX(
    sales_analytics,
    sales_analytics[price] * sales_analytics[quantity]
)
```

## 📈 Dashboards Built

1. **Total Revenue (KPI Card)**

2. **Sales by Region (Bar Chart)**

3. **Sales by Category (Pie Chart)**

4. **Top Products (Table)**

5. **Payment Method Distribution (Donut Chart)**

6. **Sales Trend over Time (Line Chart)**

## 🚀 Key Features

1. **Fully automated ETL pipeline**

2. **Secure AWS VPC networking**

3. **Scalable cloud data warehouse**

4. **Real-time BI dashboards**

5. **Enterprise-grade data engineering architecture**

## 🧑‍💻 Use Cases

1. **Sales performance tracking**

2. **Business intelligence**

3. **Financial reporting**

4. **Data engineering portfolios**

5. **Cloud analytics demonstrations**


## 📌 Future Enhancements

1. **Add AWS Lambda for event-based automation**

2. **Enable incremental data loading**

3. **Add streaming data support**

4. **Integrate authentication for dashboards**

5. **Add data quality checks**


## 🧑‍💻 Author

Arya Agrawal

GitHub: [AryaAgrawal](https://github.com/Aaryagrawal)

LinkedIn: [AryaAgrawal](https://www.linkedin.com/in/aaryaagrawal65/)
