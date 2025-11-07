# Complete Guide: Launching EC2 with Apache Web Server

## Table of Contents
1. [Creating EC2 Instance](#creating-ec2-instance)
2. [Setting up Apache on Linux](#linux-setup)
3. [Setting up Apache on Windows](#windows-setup)
4. [Creating and Deploying HTML File](#html-setup)

## Creating EC2 Instance {#creating-ec2-instance}

### Step 1: Launch EC2 Instance
1. Log in to AWS Console
2. Go to EC2 Dashboard
3. Click "Launch Instance"

### Step 2: Choose AMI (Amazon Machine Image)
For Linux:
- Select "Amazon Linux 2023" (Free tier eligible)

For Windows:
- Select "Microsoft Windows Server 2022" (Free tier eligible)

### Step 3: Choose Instance Type
- Select "t2.micro" (Free tier eligible)

### Step 4: Configure Security Group
Create new security group with these rules:
- SSH (Port 22) - For Linux access
- RDP (Port 3389) - For Windows access
- HTTP (Port 80) - For web server
- HTTPS (Port 443) - For secure web server

### Step 5: Create Key Pair
- Create new key pair
- Download the .pem file (Linux) or get password (Windows)
- Keep it safe - you'll need it to connect

### Step 6: Launch Instance
- Review and Launch
- Wait for instance to be in "running" state