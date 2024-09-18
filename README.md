# VMware based Ubuntu Server and Fullstack Application Deployment Setup Guide

This guide covers how to:
1. Install VMware on macOS
2. Create an Ubuntu VM
3. Set up Python and Next.js Application
4. Install PostgreSQL as a database
5. Install and configure Nginx as a web server

---

## 1. Install VMware on macOS

1. **Download VMware Fusion:**
   - Download the latest version of VMware Fusion from the [VMware official website](https://www.vmware.com/products/fusion.html).

2. **Install VMware Fusion:**
   - Open the `.dmg` file and follow the installation instructions.

---

## 2. Create an Ubuntu VM

1. **Download Ubuntu ISO:**
   - Go to the [Ubuntu website](https://ubuntu.com/download/desktop) and download the latest Ubuntu Desktop ISO (preferably the LTS version).

2. **Create a New Virtual Machine in VMware Fusion:**
   - Open VMware Fusion and click on `File` > `New`.
   - Choose `Install from disc or image` and select the Ubuntu ISO you downloaded.
   - Allocate resources (e.g., 2 CPU cores, 4GB RAM, and 20GB of disk space).
   - Finish the VM creation.

3. **Install Ubuntu:**
   - Follow the on-screen instructions to install Ubuntu inside the VM.
   - Set up your language, time zone, and username.

4. **Install VMware Tools:**
   - After Ubuntu is installed, go to `Virtual Machine` > `Install VMware Tools` in the VMware Fusion menu.
   - Follow the on-screen steps to install it inside Ubuntu for better performance.

---  

## Cloning project to the Server  
Create SSH key in your server and add it in the Github to clone the project to server
```bash
ssh-kygen -t ed25519
```
and press Enter after confirming the location and pasphrase for the key

```bash
cat ~/.ssh/id_ed25519.pub
```
Copy this key and go to you github "Settings'' and them go to the "SSH & GPG Keys" section and add your server ssh key  

Then move to your project and copy the SSH clone command and run on server  

```bash
apt install git -y
```
```bash
git clone --your-git ssh-key-here
```

## 3. Set Up Python and Next.js Application

### 3.1 Update System and Install Required Packages

```bash
sudo apt update && sudo apt upgrade -y
```

### 3.2 Install Python and Dependencies
Install Python 3:

```bash
sudo apt install python3 python3-pip python3-venv python3-dev -y
```

Create a Virtual Environment:

```bash
cd /path/to/your/project
```
```bash
python3 -m venv venv
```
```bash
source venv/bin/activate
```

Install Python Dependencies: If you have a requirements.txt file:

```bash
pip install -r requirements.txt
```
Install Additional Build Tools:

```bash
sudo apt install build-essential libssl-dev libffi-dev
```

### 3.3 Install Node.js for Ext.js Application
Install Node.js and npm:

```bash
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
```
```bash
sudo apt install -y nodejs
```
Verify Installation:

```bash
node -v
```
```bash
npm -v
```
Install Next.js CLI (if needed):

```bash
npm install -g sencha
```

## 4. Install and Set Up PostgreSQL
### 4.1 Install PostgreSQL
```bash
sudo apt install postgresql postgresql-contrib -y
```

## 4.2 Configure PostgreSQL
Log in to the PostgreSQL prompt:

```bash
sudo -u postgres psql
```

Create a new database and user:

```sql
CREATE DATABASE your_db_name;
```
```sql
CREATE USER your_user_name WITH PASSWORD 'your_password';
```
```sql
ALTER ROLE your_user_name SET client_encoding TO 'utf8';
```
```sql
ALTER ROLE your_user_name SET default_transaction_isolation TO 'read committed';
```
```sql
ALTER ROLE your_user_name SET timezone TO 'UTC';
```
```sql
GRANT ALL PRIVILEGES ON DATABASE your_db_name TO your_user_name;
\q
```

Allow Remote Access (Optional): Edit the PostgreSQL configuration file /etc/postgresql/12/main/pg_hba.conf and set the following:
```conf
host    all             all             0.0.0.0/0               md5
```
Restart PostgreSQL:

```bash
sudo systemctl restart postgresql
```

## 5. Install and Configure Nginx
### 5.1 Install Nginx
```bash
sudo apt install nginx -y
```

### 5.2 Configure Nginx for the Python/Ext.js Application
Create a new configuration file for your site:

```bash
sudo nano /etc/nginx/sites-available/your_project
```
Nginx Configuration for Proxying to Python and Serving Next.js Files:

Example Nginx configuration:

```nginx
server {
    listen 80;
    server_name your_domain.com www.your_domain.com;

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    location /static/ {
        alias /path/to/your/static/files/;  # Path where Ext.js static files are located
    }

    location /media/ {
        alias /path/to/your/media/files/;  # If any media files need to be served
    }

    # SSL configuration (if needed)
    # listen 443 ssl;
    # ssl_certificate /etc/nginx/ssl/your_domain.com.crt;
    # ssl_certificate_key /etc/nginx/ssl/your_domain.com.key;
}
```
Enable the Configuration:

```bash
sudo ln -s /etc/nginx/sites-available/your_project /etc/nginx/sites-enabled/
```
```bash
sudo nginx -t  # Test the configuration for syntax errors
```
Restart Nginx:

```bash
sudo systemctl restart nginx
```

## 6. Final Steps
### 6.1 Running Your Python Application

To run your Python application (for Django/Flask):

(to be added)

## 7. Additional Notes
Make sure to configure a firewall (e.g., ufw) to allow traffic on port 80 (and 443 if using SSL).
If SSL is required, use Let's Encrypt to set up free SSL certificates:
```bash
sudo apt install certbot python3-certbot-nginx
```
```bash
sudo certbot --nginx -d your_domain.com -d www.your_domain.com
```

```python

This guide should help you set up everything required for your POC. Let me know if any part needs further clarification or additional details!





