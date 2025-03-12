Step 1: Set Up DVWA on AWS EC2
Launch an AWS EC2 instance

Choose Ubuntu 22.04 LTS (Free Tier Eligible)
Instance Type: t2.micro
Storage: 8GB
Security Group:
Allow HTTP (80), HTTPS (443), SSH (22)
Restrict SSH to My IP
Download the key pair for SSH access.
Connect to EC2 via SSH:

bash
Copy
Edit
ssh -i your-key.pem ubuntu@your-ec2-public-ip
Install required packages:

bash
Copy
Edit
sudo apt update && sudo apt install -y apache2 mariadb-server php php-mysql unzip git
Clone and set up DVWA:

bash
Copy
Edit
cd /var/www/html
sudo git clone https://github.com/digininja/DVWA.git
sudo chown -R www-data:www-data DVWA
Configure MySQL database:

bash
Copy
Edit
sudo mysql -u root -e "CREATE DATABASE dvwa;"
sudo mysql -u root -e "CREATE USER 'dvwa'@'localhost' IDENTIFIED BY 'password';"
sudo mysql -u root -e "GRANT ALL PRIVILEGES ON dvwa.* TO 'dvwa'@'localhost';"
sudo mysql -u root -e "FLUSH PRIVILEGES;"
Restart Apache and access DVWA:

bash
Copy
Edit
sudo systemctl restart apache2
Open http://your-ec2-public-ip/DVWA/
Login: admin / password
Set Security Level to "Low" for testing.