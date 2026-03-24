# aws-web-app-deployment
AWS EC2 + S3 + VPC + IAM Project

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
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AWS Web App Project</title>

    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(to right, #4facfe, #00f2fe);
            color: #333;
        }

        header {
            background: #222;
            color: white;
            padding: 15px 0;
            text-align: center;
        }

        header h1 {
            margin-bottom: 5px;
        }

        nav {
            margin-top: 10px;
        }

        nav a {
            color: white;
            margin: 0 15px;
            text-decoration: none;
            font-size: 14px;
        }

        nav a:hover {
            text-decoration: underline;
        }

        .container {
            padding: 40px;
            text-align: center;
        }

        .box {
            background: white;
            padding: 30px;
            border-radius: 10px;
            display: inline-block;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
            margin-top: 40px;
        }

        .box h2 {
            margin-bottom: 15px;
            color: #444;
        }

        .box p {
            font-size: 16px;
            margin-bottom: 20px;
        }

        .btn {
            background: #4facfe;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        .btn:hover {
            background: #007bff;
        }

        .section {
            margin-top: 60px;
        }

        .card-container {
            display: flex;
            justify-content: center;
            gap: 20px;
            flex-wrap: wrap;
        }

        .card {
            background: white;
            padding: 20px;
            width: 250px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
        }

        .card h3 {
            margin-bottom: 10px;
        }

        footer {
            margin-top: 60px;
            background: #222;
            color: white;
            text-align: center;
            padding: 15px;
        }
    </style>
</head>

<body>

<header>
    <h1>🚀 AWS Web App Deployment</h1>
    <p>EC2 + S3 + VPC + IAM Project</p>

    <nav>
        <a href="#">Home</a>
        <a href="#">Project</a>
        <a href="#">Services</a>
        <a href="#">Contact</a>
    </nav>
</header>

<div class="container">

    <div class="box">
        <h2>Welcome to My AWS Project</h2>
        <p>This web application is deployed using AWS services.</p>
        <button class="btn" onclick="showMessage()">Click Me</button>
    </div>

    <div class="section">
        <h2>📦 Services Used</h2>

        <div class="card-container">

            <div class="card">
                <h3>EC2</h3>
                <p>Virtual server used to host the web application.</p>
            </div>

            <div class="card">
                <h3>S3</h3>
                <p>Storage service used to store static files.</p>
            </div>

            <div class="card">
                <h3>VPC</h3>
                <p>Custom network setup for secure deployment.</p>
            </div>

            <div class="card">
                <h3>IAM</h3>
                <p>Manages access and permissions securely.</p>
            </div>

        </div>
    </div>

</div>

<footer>
    <p>© 2026 AWS Project | Created by Mahaksh</p>
</footer>

<script>
    function showMessage() {
        alert("🎉 Your AWS Web App is working perfectly!");
    }
</script>

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
