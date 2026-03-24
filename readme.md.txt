# 🚀 AWS Web App Deployment Project (EC2 + S3 + VPC + IAM)

## 📌 Project Overview

This project demonstrates how to deploy a simple static web application using core AWS services.
The website is stored in S3 and hosted on an EC2 instance using Apache within a custom VPC.

---

## 🏗️ Architecture

User (Browser)
↓
EC2 Public IP
↓
Apache Web Server
↓
HTML File (from S3)

---

## 📂 Step-by-Step Implementation

---

### 🔹 Step 1: Create Web Application

Create a file named `index.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My AWS Project</title>
</head>
<body>
    <h1>🚀 My First AWS Web App</h1>
    <p>Deployed using EC2 + S3 + VPC + IAM</p>
</body>
</html>
```

---

### 🔹 Step 2: Setup VPC (Networking)

* Create VPC

  * CIDR: 10.0.0.0/16

* Create Subnet

  * CIDR: 10.0.1.0/24

* Create Internet Gateway

* Attach IGW to VPC

* Create Route Table

  * Add route: 0.0.0.0/0 → Internet Gateway

* Associate Route Table with Public Subnet

---

### 🔹 Step 3: Setup IAM Role

* Create IAM Role for EC2
* Attach policy: AmazonS3ReadOnlyAccess

---

### 🔹 Step 4: Upload File to S3

* Create S3 bucket (unique name)
* Upload `index.html`
* Make file public (via bucket policy)

Correct Object URL format:

```
https://your-bucket-name.s3.eu-north-1.amazonaws.com/index.html
```

---

### 🔹 Step 5: Launch EC2 Instance

* AMI: Amazon Linux
* Instance type: t2.micro
* Enable Public IP
* Attach IAM Role

Security Group:

* SSH (22) → Anywhere
* HTTP (80) → Anywhere

---

### 🔹 Step 6: Install Apache Web Server

Connect to EC2 and run:

```bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```

---

### 🔹 Step 7: Deploy Website from S3

```bash
cd /var/www/html
sudo rm index.html
sudo curl -O https://your-bucket-name.s3.eu-north-1.amazonaws.com/index.html
sudo systemctl restart httpd
```

---

### 🔹 Step 8: Access Website

Open in browser:

```
http://<EC2-Public-IP>
```

---

## ⚠️ Challenges Faced

* Internet Gateway not attached
* Route table not configured properly
* Apache not installed (connection refused)
* S3 TemporaryRedirect error (fixed using correct region URL)

---

## 🧠 Key Learnings

* VPC networking (Subnet, IGW, Route Table)
* IAM roles and permissions
* Hosting static files in S3
* Web server setup using EC2
* Troubleshooting AWS errors

---


## 🔮 Future Improvements

* Add Load Balancer
* Enable HTTPS (SSL)
* Implement Auto Scaling
* Secure S3 (private access via IAM)

---
