# Linux EC2 Setup Guide with Apache

## Connecting to Linux Instance

### Step 1: Connect to Your Instance
```bash
ssh -i "your-key.pem" ec2-user@your-instance-public-ip
```
Command Explanation:
- `ssh`: Secure Shell protocol for secure connection
- `-i`: Specifies the identity file (your private key)
- `ec2-user`: Default user for Amazon Linux
- `your-instance-public-ip`: Your EC2's public IP address

### Step 2: Update System
```bash
sudo yum update -y
```
Command Explanation:
- `sudo`: Run command with root privileges
- `yum`: Package manager for Amazon Linux
- `update`: Command to update package lists
- `-y`: Automatically answer yes to prompts

### Step 3: Install Apache
```bash
sudo yum install httpd -y
```
Command Explanation:
- `httpd`: Apache web server package name
- `-y`: Automatically confirm installation

### Step 4: Start Apache Service
```bash
sudo systemctl start httpd
sudo systemctl enable httpd
```
Command Explanation:
- `systemctl start`: Starts the Apache service
- `systemctl enable`: Makes Apache start automatically on boot

### Step 5: Check Apache Status
```bash
sudo systemctl status httpd
```
Command Explanation:
- Shows if Apache is running correctly
- Displays any errors if present

## Creating and Deploying HTML File

### Step 1: Navigate to Web Directory
```bash
cd /var/www/html
```
Command Explanation:
- Default Apache web root directory
- Where your web files should be placed

### Step 2: Create HTML File
```bash
sudo nano index.html
```
Command Explanation:
- `nano`: Text editor (easy to use)
- Creates/edits index.html file

### Step 3: Add Basic HTML Content
```html
<!DOCTYPE html>
<html>
<head>
    <title>My AWS Website</title>
</head>
<body>
    <h1>Welcome to my AWS EC2 Website!</h1>
    <p>This site is hosted on Amazon EC2 with Apache.</p>
</body>
</html>
```

### Step 4: Save File
In nano:
- Press CTRL + X
- Press Y to confirm
- Press Enter to save

### Step 5: Set Permissions
```bash
sudo chmod 644 index.html
```
Command Explanation:
- `chmod`: Changes file permissions
- `644`: Owner can read/write, others can only read

## Access Your Website
- Open browser
- Enter your EC2 public IP address
- You should see your webpage

## Troubleshooting Commands
```bash
# Check Apache error logs
sudo tail -f /var/log/httpd/error_log

# Check Apache configuration
sudo apachectl configtest

# Restart Apache if needed
sudo systemctl restart httpd
```