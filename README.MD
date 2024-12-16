# Steps to Provision and Configure the Server
### 1. Create an EC2 Instance on AWS
### 2. Install and Configure the Apache Web Server
### 3. Deploy an HTML Page
### 4. Configure Networking for HTTP Traffic
### 5. Configure HTTPS Using free Let’s Encrypt (Certbot)
### 6. Access the Website


## 1. Create an EC2 Instance on AWS
Launched an Ubuntu EC2 instance on AWS with a security group allowing SSH and HTTP traffic.
Connected to the instance via SSH using a private key.

- Instance Type: Ubuntu Linux (free tier eligible).
- Security Group Configuration: Added inbound rule to allow SSH traffic on port 22.
- SSH Setup:
Used Termius as my SSH terminal.
- Ensured my private key file permissions were secure (not publicly viewable) using:
```bash
chmod 400 <Keypair.pem>
```
- Connected to the instance via its public DNS using:
```bash
ssh -i <Keypair.pem> ubuntu@<instance-public-DNS>
```

## 2. Install and Configure the Apache Web Server
Apache is a widely used web server for hosting websites. After updating the system, Apache was installed. This installation sets up a reliable environment for serving web content. The default document root is /var/www/html, where website files, like HTML, are stored. After installation, the Apache service was started automatically, making it ready to serve the uploaded content.
- Updated the system packages using:
```bash
sudo apt update 
```
- Installed Apache using:
```bash
sudo apt install apache2 -y
```
- Checked Apache status using:
```bash
sudo systemctl status apache2
```

## 3. Deploy an HTML Page
Created the webpage using Visual Studio Code and pushed it to GitHub. Downloadad the repository on the server and copied URL to the zip file of the repository, downloaded and unzipped the zip file of the HTML file to the Apache document root
- Downloaded the zip file of the repository using:
```bash
wget <zip_file>
```
- Checked the list of files using:
```bash
ls
```
- Installed unzip
```bash
sudo apt install unzip
```
- Installed unzip
```bash
sudo unzip <zip_file>
```
- Checked the list of files using:
```bash
ls
```
- Copied the HTML file to the Apache document root using:
```bash
sudo cp -r * /var/www/html
```
## 4. Configure Networking for HTTP Traffic
Updated the security group to allow inbound traffic on port 80.
Registered a subdomain via FreeDNS and mapped it to the instance's public IP.
- Security Group Configuration: Added an inbound rule to allow HTTP (port 80) traffic.
- Domain Routing:
Registered a free subdomain on FreeDNS.
- Mapped the public IP to the subdomain 
```
http://olacloud.mooo.com/
```

## 5. Configure HTTPS Using free Let’s Encrypt (Certbot)
Updated the security group to allow inbound traffic on port 443. Installed Certbot SSL certificate for HTTPS configuration of the web server.
- Updated the system packages using:
```bash
sudo apt update
```
- Installed Certbot
```bash
sudo apt install certbot python3-certbot-apache -y
```
- Obtained SSL Certificate: Ran Certbot to automatically configure HTTPS using:
```bash
sudo certbot --apache
```
- Verified and tested configuration of Certbot SSL certificate 
```bash
sudo apache2ctl configtest
```
- Restarted Apache web server
```bash
sudo systemctl restart apache2
```
- Enabled auto-renewal of Certbot SSL on https://olacloud.mooo.com
```bash
sudo certbot renew --dry-run
```

## 6. Access the Website
- Public IP: 
```
http://204.236.250.172/
```
- Custom Domain: 
```
https://olacloud.mooo.com/
```