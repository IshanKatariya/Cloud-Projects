## 🎓 Student Registration System (AWS Full-Stack Project)

A fully deployed cloud-based student registration system built using Flask, AWS EC2, Amazon RDS (MySQL) and cloud networking.
The application allows students to register via a web form, stores data securely in RDS, and provides an admin dashboard to view all records.

## 🔥 Live Project Features

**1. Student Registration:**  Web form collects name, email, course & age

**2. Cloud Database:**	 Data stored in Amazon RDS (MySQL)

**3. Flask Backend:**	 Handles form submission & DB operations

**4. Admin Dashboard:**	 View all registered students in a table

**5. Cloud Deployment:**	 Deployed on AWS EC2 with public IP

**6. Secure Architecture:**	 EC2 ↔ RDS communication via Security Groups

## 🖥️ Screenshots (Project Proof)


**1. Hosted on EC2:**	Reads data from Amazon RDS
    

**2. Form → Flask → MySQL:** Displays student records

<img width="1364" height="718" alt="image" src="https://github.com/user-attachments/assets/1c3f1380-c623-457f-b05a-0bb551bd6bdf" />

<img width="1350" height="321" alt="image" src="https://github.com/user-attachments/assets/bde442c0-8f7f-47be-b733-4e8130c3a0d4" />

![WhatsApp Image 2026-01-08 at 6 00 43 PM](https://github.com/user-attachments/assets/7246d425-deaf-471d-85e5-bb11ec1aa9c2)

<img width="1362" height="667" alt="image" src="https://github.com/user-attachments/assets/77126475-87c3-4755-b70c-985267993cc8" />

![WhatsApp Image 2026-01-08 at 5 49 02 PM](https://github.com/user-attachments/assets/9d2c31af-2ce9-46e9-b81a-b08600ab94c9)


## 🧱 Tech Stack

**1.Frontend:**	HTML, CSS

**2.Backend:** Flask (Python)

**3.Database:**	Amazon RDS (MySQL)

**4.Cloud Server:**	AWS EC2

**5.Networking:**	AWS Security Groups

**6.OS:**	Amazon Linux

**7.Deployment:**	Gunicorn + Flask

## 🧠 System Architecture

<img width="1021" height="450" alt="Cloud Project ( FULLL WEB APP ) architecture" src="https://github.com/user-attachments/assets/65248ce0-d79b-4674-b719-9b48879d53ab" />


User Browser
     |
     |  (HTTP Request)
     v
AWS EC2 (Flask App)
     |
     |  (MySQL Query)
     v
Amazon RDS (MySQL Database)
     |
     |  (Results)
     v
AWS EC2 → User Browser


This is a true production-style 3-tier cloud application.




## 🧪 Sample Data Stored

ID	        Name	        Email	            Course	Age

1	          Aarya Agarwal	aarya@gmail.com   BCA	    21


This data is live inside Amazon RDS.

## 🚀 How It Works

1. User opens EC2 public IP

2. Registration form loads

3. User submits details

4. Flask validates data

5. Data stored in Amazon RDS

6. Admin accesses /admin

7. Flask queries MySQL

8. Table renders live student data



🧑‍💻 Author

Aarya Agrawal

GitHub: [AaryaAgrawal](https://github.com/Aaryagrawal)

LinkedIn: [AaryaAgrawal](https://www.linkedin.com/in/aaryaagrawal65/)
