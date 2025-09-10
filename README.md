## Deploying a Static Website on AWS EC2 using Apache and nano

This guide walks through launching a static website on an Ubuntu EC2 instance, installing Apache, and creating your homepage using nano. All steps are accompanied by relevant command-line examples for beginners.[1]

***

### Prerequisites

- AWS Account
- Basic knowledge of command line
- SSH client (like PowerShell, Terminal)

***

### Step 1: Create a Key Pair

```sh
# In AWS Console
# Navigate to EC2 → Key pairs → Create key pair
# Set Name: Keypair_1, Type: RSA, and Private key format: .pem
```
- Download and save `Keypair_1.pem` safely.[1]

***

### Step 2: Set Up Security Group

```sh
# In AWS Console
# EC2 → Security Groups → Create security group
# Name: Web-SG
# Description: Allow SSH from my IP and HTTP from anywhere
# Inbound Rules:
#   SSH: Port 22, Source: My IP
#   HTTP: Port 80, Source: Anywhere (0.0.0.0/0)
```
- Leave outbound rules as default.[1]

***

### Step 3: Create a Subnet

```sh
# VPC → Subnets → Create subnet
# Select VPC, Name: Public-Subnet-1
# Availability Zone: (e.g., us-east-1a)
# IPv4 CIDR block: 172.31.1.0/24
```


***

### Step 4: Launch EC2 Instance

```sh
# EC2 Dashboard → Launch Instance
# Name: apache-web-01
# AMI: Ubuntu Server
# Instance type: t3.micro (Free Tier eligible)
# Network: Select your VPC
# Subnet: Public-Subnet-1
# Auto-assign Public IPv4: Enable
# Storage: 8 GiB gp3 or gp2
# Security Group: Web-SG
# Key Pair: Keypair_1
```
- Review and Launch, wait until status is "running".[1]

***

### Step 5: Connect via SSH

```sh
ssh -i "Keypair_1.pem" ubuntu@<EC2_PUBLIC_IP>
```
- If prompted, type `yes` when asked to continue connecting.[1]

***

### Step 6: Install Apache Web Server

Update package list:
```sh
sudo apt update
```
Install Apache:
```sh
sudo apt install apache2 -y
```
Start and enable Apache:
```sh
sudo systemctl start apache2
sudo systemctl enable apache2
```
Check status:
```sh
sudo systemctl status apache2
```


***

### Step 7: Create Your Homepage

Open the default HTML file in nano:
```sh
sudo nano /var/www/html/index.html
```
Delete existing lines (press `Ctrl + K` repeatedly), then write:
```html
<!doctype html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>My AWS Apache Site</title>
  <style>body{font-family:system-ui;margin:2rem;}</style>
</head>
<body>
  <h1>It works! 🚀</h1>
  <p>Served by Apache on AWS EC2.</p>
</body>
</html>
```
Save and exit nano:
- `Ctrl + O` then Enter (Save)
- `Ctrl + X` (Exit)[1]

Reload Apache (optional if editing static HTML):
```sh
sudo systemctl reload apache2
```
Or if reload fails:
```sh
sudo systemctl restart apache2
```


***

### Step 8: View Your Website

Open in browser:
```
http://<EC2_PUBLIC_IP>
```
You should see the Apache default page or your custom homepage.[1]

***

## Socials

<a href="https://github.com/ShaikhAteeb02" target="_blank"><img src="https://img.shields.io/badge/GitHub-profile-black?logo=github" alt="GitHub"></a>
<a href="https://www.linkedin.com/in/ateeb-ahmed-shaikh-932234192" target="_blank"><img src="https://img.shields.io/badge/LinkedIn-profile-blue?logo=linkedin" alt="LinkedIn"></a>
