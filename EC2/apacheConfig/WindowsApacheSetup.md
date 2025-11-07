# Windows EC2 Setup Guide with Apache

## Connecting to Windows Instance

### Step 1: Get Windows Password
1. Select your instance in EC2 Console
2. Click "Connect"
3. Choose "RDP Client"
4. Click "Get Password"
5. Upload your .pem key file
6. Click "Decrypt Password"
7. Save the password

### Step 2: Connect via RDP
1. Open Remote Desktop Connection
2. Enter your instance's public IP
3. Use credentials:
   - Username: Administrator
   - Password: (decrypted password)

## Installing Apache on Windows

### Step 1: Download Apache
1. Go to https://www.apachelounge.com/download/
2. Download Apache 2.4 (VC17) ZIP file
3. Extract to C:\Apache24

### Step 2: Install Apache as a Service
Open Command Prompt as Administrator and run:
```cmd
cd C:\Apache24\bin
httpd.exe -k install
```
Command Explanation:
- `cd`: Change directory to Apache bin folder
- `httpd.exe -k install`: Installs Apache as a Windows service

### Step 3: Configure Apache
1. Edit C:\Apache24\conf\httpd.conf
2. Find "ServerRoot" line and confirm it's:
```apache
ServerRoot "c:/Apache24"
```
3. Find "Listen" line and confirm it's:
```apache
Listen 80
```

### Step 4: Start Apache Service
In Command Prompt as Administrator:
```cmd
net start Apache2.4
```
Command Explanation:
- Starts the Apache service in Windows

## Creating and Deploying HTML File

### Step 1: Navigate to Web Directory
The default web root is: C:\Apache24\htdocs

### Step 2: Create index.html
Create a file named index.html with this content:
```html
<!DOCTYPE html>
<html>
<head>
    <title>My AWS Windows Website</title>
</head>
<body>
    <h1>Welcome to my AWS EC2 Windows Website!</h1>
    <p>This site is hosted on Windows EC2 with Apache.</p>
</body>
</html>
```

## Access Your Website
- Open browser
- Enter your EC2 public IP address
- You should see your webpage

## Troubleshooting Commands
```cmd
# Check Apache service status
services.msc
(Look for Apache2.4 service)

# Restart Apache
net stop Apache2.4
net start Apache2.4

# Check error logs
C:\Apache24\logs\error.log
```

## Important Notes
1. Make sure Windows Firewall allows port 80
2. Keep Windows and Apache updated
3. Set proper security permissions on htdocs folder
4. Monitor Windows Event Viewer for issues