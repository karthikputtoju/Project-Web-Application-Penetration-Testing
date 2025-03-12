## Hands-On Task Checklist for Web Application Penetration Testing

Use this checklist to track your progress. Each task corresponds to different security testing techniques.

### 🛠 1. Setup - Deploy the Target Application

| #  | Task                                                                 | Status |
|----|----------------------------------------------------------------------|--------|
| 1  | Launch AWS EC2 instance with Ubuntu.                                 |   ☐    |
| 2  | Install Apache, MySQL, PHP (LAMP Stack).                             |   ☐    |
| 3  | Deploy DVWA / OWASP Juice Shop on the instance.                      |   ☐    |
| 4  | Configure MySQL and enable low-security settings in DVWA.            |   ☐    |
| 5  | Verify application is running at http://your-ec2-public-ip/DVWA/.    |   ☐    |

### 🔎 2. Reconnaissance - Information Gathering

| #  | Task | Command | Status |
|----|----------------------------------|----------------------------------|--------|
| 6  | Scan for open ports and services. | `nmap -sV -A your-ec2-ip` | ☐ |
| 7  | Identify web technologies in use. | `whatweb http://your-ec2-ip` | ☐ |
| 8  | Check for hidden directories. | `dirb http://your-ec2-ip` | ☐ |
| 9  | Identify potential web vulnerabilities. | `nikto -h http://your-ec2-ip` | ☐ |

### 🎯 3. Exploitation - Web Application Attacks

| #  | Task | Tool/Method | Status |
|----|----------------------------------|----------------------------------|--------|
| 10  | Perform SQL Injection & dump database. | `sqlmap -u "http://your-ec2-ip/vulnerabilities/sqli/?id=1" --dbs --batch` | ☐ |
| 11  | Exploit Cross-Site Scripting (XSS). | `<script>alert('XSS Found')</script>` via Burp Suite | ☐ |
| 12  | Conduct CSRF attack (Change password). | HTML CSRF attack form | ☐ |
| 13  | Attempt session hijacking by stealing cookies. | Burp Suite | ☐ |
| 14  | Identify broken authentication issues (login bypass, weak passwords). | Manual Testing | ☐ |

### 📜 4. Reporting - Document Findings & Mitigations

| #  | Task | Status |
|----|--------------------------------------------|--------|
| 15  | Create a penetration test report in Dradis/OpenVAS. | ☐ |
| 16  | List discovered vulnerabilities with CVSS scores. | ☐ |
| 17  | Provide security recommendations for each issue. | ☐ |
| 18  | Include evidence screenshots and proof-of-concept (PoC) exploits. | ☐ |
