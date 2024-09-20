# VMware Ubuntu Server with Fullstack Application Deployment & Nagios monitoring Setup Guide

The VMware Ubuntu Server with Fullstack Application Deployment & Nagios Monitoring Setup Guide offers a comprehensive walkthrough for setting up a virtualized Ubuntu Server using VMware. It covers the installation and configuration of a fullstack application (frontend, backend, and database), followed by the integration of Nagios for real-time monitoring. This guide includes steps for setting up the virtual environment, deploying the application, and configuring Nagios to monitor server performance and application health, ensuring a stable and scalable deployment.

### This guide covers how to:  

1. Install VMware on macOS
2. Create an Ubuntu VM
3. Set up Python and Next.js Application
4. Install PostgreSQL as a database
5. Install and configure Nginx as a web server
6. Running Python and Next.js application
7. Install Nagios on Ubuntu
8. Add a Remote Host for Monitoring in Nagios
9. Checking Logs for Python Application Deployed as a Service
10. Additional Notes

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

<img width="1000" alt="Screenshot 2024-09-19 at 4 56 56 PM" src="https://github.com/user-attachments/assets/bdb5d98c-5ee1-49ba-a329-b65c245cbead">  

- Choose `Install from disc or image`  

<img width="1000" alt="Screenshot 2024-09-19 at 4 57 30 PM" src="https://github.com/user-attachments/assets/f6250fe3-5c78-42fd-a8f8-6f8f2c9b6711">   

- Select the Ubuntu ISO you downloaded.   

<img width="1000" alt="Screenshot 2024-09-19 at 4 57 43 PM" src="https://github.com/user-attachments/assets/2978b15b-c827-4d5c-9284-5f191a10b9da">   

- Select Installation Method "Easy or Customised"
  
<img width="1000" alt="Screenshot 2024-09-19 at 4 58 20 PM" src="https://github.com/user-attachments/assets/b769aeec-4c7b-4b14-ac3b-2f0480c85070">  

- Allocate resources (e.g., 2 CPU cores, 4GB RAM, and 20GB of disk space) and Click Finish to proceed the Installation

<img width="1000" alt="Screenshot 2024-09-19 at 4 58 44 PM" src="https://github.com/user-attachments/assets/18057116-b761-4197-8077-fed9b912da60">    

4. **Install Ubuntu:**

- Setup the network configurations for the VM either bridg or DHCP wth wifi enabled or not

<img width="1000" alt="Screenshot 2024-09-19 at 5 30 44 PM" src="https://github.com/user-attachments/assets/ef9c2064-52c6-45c4-9a3a-02534963fbb6">

- Now on the Ubuntu Installation User Interface select the desired laabnguage

<img width="1000" alt="Screenshot 2024-09-19 at 5 01 31 PM" src="https://github.com/user-attachments/assets/3631f0c4-2aad-4e2d-aa43-ee7826b783b8">     

- Select any accessiblity settings for the server accordingly  

<img width="1000" alt="Screenshot 2024-09-19 at 5 01 42 PM" src="https://github.com/user-attachments/assets/84180c6d-7571-4612-810a-7edd62041599">  

- Select Internet settings for the VM

<img width="1000" alt="Screenshot 2024-09-19 at 5 01 56 PM" src="https://github.com/user-attachments/assets/00f67c78-96ff-4cf3-85b5-2e53d49fceaa">  

- Click Install Ubuntu

<img width="1000" alt="Screenshot 2024-09-19 at 5 02 05 PM" src="https://github.com/user-attachments/assets/a19cd72b-32ca-4510-8115-3deecd63e0c0">  

- Select installation type

<img width="1000" alt="Screenshot 2024-09-19 at 5 02 13 PM" src="https://github.com/user-attachments/assets/4e11ad36-3754-45c7-80d3-d2f3ba1e5e41">  

- Select any third party apps "Default" or "Extended" selection
  
<img width="1000" alt="Screenshot 2024-09-19 at 5 02 25 PM" src="https://github.com/user-attachments/assets/0337b9a9-fd59-4183-8185-a26eddae7884">  

- Choose if you want to install any proprietry softwares along with the OS

<img width="1000" alt="Screenshot 2024-09-19 at 5 02 36 PM" src="https://github.com/user-attachments/assets/b0631db1-d87c-4535-96a3-f89140b2ce49">  

- Choose storage operations for the VM

<img width="1000" alt="Screenshot 2024-09-19 at 5 03 14 PM" src="https://github.com/user-attachments/assets/fbc57d51-1b78-4c23-8edb-ae58e948f8c3">  

- Creat your account for the server

<img width="1000" alt="Screenshot 2024-09-19 at 5 03 59 PM" src="https://github.com/user-attachments/assets/4db3a489-05db-4f1b-ab9a-6a561a5f197b">  

- Select your desired timezone

<img width="1000" alt="Screenshot 2024-09-19 at 5 04 07 PM" src="https://github.com/user-attachments/assets/99bc3672-267e-4248-bedb-e7a4ee9669fb">   

- Review all details and proceed with the OS installation

<img width="1000" alt="Screenshot 2024-09-19 at 5 04 18 PM" src="https://github.com/user-attachments/assets/ac3c458a-4fe6-45ec-bdca-0ce4dcb5a45e"> 

- Finish the VM creation.

5. **Install VMware Tools:**
   - After Ubuntu is installed, go to `Virtual Machine` > `Install VMware Tools` in the VMware Fusion menu.
   - Follow the on-screen steps to install it inside Ubuntu for better performance.

---  


## 3. Cloningg the project and Set Up of Python and Next.js Application  

### 3.1 Cloning project to the Server  
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


### 3.2 Update System and Install Required Packages

```bash
sudo apt update && sudo apt upgrade -y
```

### 3.3 Install Python and Dependencies
Install Python 3:

```bash
sudo apt install python3 python3-pip python3-venv python3-dev python3-dev python3-distutils -y
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

Install Python Dependencies:

```bash
poetry install
```
Install Additional Build Tools:

```bash
sudo apt install build-essential libssl-dev libffi-dev
```

### 3.4 Install Node.js for Next.js Application
Install NVM for Node and npm:  

```bash
apt install curl
```
```bash
ccurl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```
```bash
export NVM_DIR="$HOME/.nvm"
15  [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
16  [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"
```
Verify Installation:

```bash
nvm -v
```
```bash
nvm install 18.20.3
node -v
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
        return 301 https://$host$request_uri;
    }
}

server {
    listen 443 ssl http2;
    server_name your_domain.com www.your_domain.com;

    ssl_certificate /etc/letsencrypt/live/your_domain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/your_domain.comprivkey.pem;
   # add_header Access-Control-Allow-Origin *;
   # add_header Access-Control-Allow-Methods *;
   # add_header Access-Control-Allow-Headers *;


        location / {
        proxy_pass http://127.0.0.1:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }


   location /_next/webpack-hmr {
    proxy_pass http://localhost:3000;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}
    }
    server {
    listen 80;
    server_name your_domain.com www.your_domain.com;
    location / {
        return 301 https://$host$request_uri;
    }
}
}

server {
    listen 443 ssl;
    server_name your_domain.com www.your_domain.com;

    ssl_certificate /etc/letsencrypt/live/your_domain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/your_domain.com/privkey.pem;
    #add_header Access-Control-Allow-Origin *;
    #add_header Access-Control-Allow-Methods *;
    #add_header Access-Control-Allow-Headers *;


        location / {
        #proxy_pass http://127.0.0.1:8081;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Connection "keep-alive";
        proxy_buffering off;

        proxy_read_timeout 3600s;
        proxy_send_timeout 3600s;
        proxy_set_header Transfer-Encoding $http_transfer_encoding;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
       # proxy_set_header Access-Control-Allow-Origin *;

        proxy_pass http://127.0.0.1:8081;

    }
    location /_next/webpack-hmr {
    proxy_pass http://127.0.0.1:8081;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}

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

## 6. Running Python and Next.js application
### 6.1 Creating the service file for Running Your Python Application

Add the Database credeenrtials and other secret details in your .env file and test the project  
```bash
make start
```

Now create a service file in the below location to run the python project as a service  in linux  
```bash
vim /etc/systemd/system/mypythonproject.service
```
and Enter the below configurations to run the project  

```bash
[Unit]
Description=Python Backend
After=network.target

[Service]
User=root
WorkingDirectory=/root/Backend-application
ExecStart=/bin/bash -c 'make start'
Restart=always

[Install]
WantedBy=multi-user.target
```
Verify python service status
```bash
systemctl start python.service
```
```bash
systemctl status python.serrvice
```
### 6.2 Running the Next.js Frontend using the pm2  

Switch to the frontend project
```basah
cd /path/to/your/frontend
```
Now add the backend details in the .env of the project
```bash
vim .env
```
Test the frontend
```bash
npm run start
```
Once everything is good Install the pm2 and run the frontend in the backgroundd process using it
```bash
npm install pm2 --location=global
```
Run the frontend
```bash
pm2 start "npm start" --name frontend
```
Verify it in the browser by copying your IP address and pasting with the port application running on  
```bash
http://192.1681.123.321:3000
```

## 7. Install Nagios on Ubuntu
### 7.1 Update Your System
Start by updating the package list and upgrading the installed packages:

```bash
sudo apt update && sudo apt upgrade -y
```
### 7.2 Install Prerequisites
Nagios requires some dependencies, including Apache, PHP, and additional libraries:

```bash
sudo apt install wget build-essential apache2 php libapache2-mod-php php-gd libgd-dev unzip -y
```

### 7.3 Create a Nagios User and Group
Create a Nagios user and group, and add the Apache user to the Nagios group:

```bash
sudo useradd nagios
```
```bash
sudo groupadd nagcmd
```
```bash
sudo usermod -aG nagcmd nagios
```bash
sudo usermod -aG nagcmd www-data
```

### 7.4 Download and Install Nagios Core
Download Nagios Core:

```bash
cd /tmp
```
```bash
wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.4.6.tar.gz
```
```bash
tar -zxvf nagios-4.4.6.tar.gz
```
```bash
cd nagios-4.4.6
```

Compile and Install Nagios:

```bash
sudo ./configure --with-command-group=nagcmd
```
```bash
sudo make all
```
```bash
sudo make install
```
```bash
sudo make install-commandmode
```
```bash
sudo make install-init
```
```bash
sudo make install-config
```
```bash
sudo make install-webconf
```

### 7.5 Install Nagios Plugins
Download and Install Plugins:

```bash
cd /tmp
```
```bash
wget https://nagios-plugins.org/download/nagios-plugins-2.3.3.tar.gz
```
```bash
tar -zxvf nagios-plugins-2.3.3.tar.gz
```
```bash
cd nagios-plugins-2.3.3
```
```bash
sudo ./configure --with-nagios-user=nagios --with-nagios-group=nagios --with-openssl
```
```bash
sudo make
```
```bash
sudo make install
```

### 7.6 Configure Apache for Nagios
Create a Nagios Admin User:

```bash
sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin
```
(You will be prompted to enter a password for the nagiosadmin user.)

Enable Apache Modules and Restart Apache:

```bash
sudo a2enmod rewrite cgi
```
```bash
sudo systemctl restart apache2
```

### 7.7 Start and Enable Nagios Service
Start Nagios and Enable it to Start on Boot:

```bash
sudo systemctl start nagios
```
```bash
sudo systemctl enable nagios
```

Verify Nagios is Running:

Open a web browser and navigate to http://<your-server-ip>/nagios. Log in with the username nagiosadmin and the password you set.

## 8. Add a Remote Host for Monitoring
To monitor another machine (let's call it Remote Host), you need to install Nagios NRPE (Nagios Remote Plugin Executor) on that machine and configure it.

### 8.1 Install NRPE on the Remote Host
Install NRPE and Nagios Plugins:

On the Remote Host (another Ubuntu server), run:

```bash
sudo apt update
```
```bash
sudo apt install nagios-nrpe-server nagios-plugins -y
```

Configure NRPE:

Edit the NRPE configuration file:

```bash
sudo nano /etc/nagios/nrpe.cfg
```

Add the IP address of your Nagios Server to the allowed_hosts directive:

```bash
allowed_hosts=<Nagios_Server_IP>,127.0.0.1
```
Save and exit the file.  

Restart NRPE Service:

```bash
sudo systemctl restart nagios-nrpe-server
```
```bash
sudo systemctl enable nagios-nrpe-server
```

### 8.2 Configure Nagios Server to Monitor Remote Host
Create a Configuration File for the Remote Host:

On the Nagios Server:

```bash
sudo nano /usr/local/nagios/etc/servers/<remote_host_name>.cfg
```

Replace <remote_host_name> with the actual name of the remote host.

Define the Remote Host and Services to Monitor:

Example configuration:

```bash
define host {
    use             linux-server
    host_name       <remote_host_name>
    alias           <remote_host_alias>
    address         <Remote_Host_IP>
    max_check_attempts 5
    check_period    24x7
    notification_interval 30
    notification_period  24x7
}

define service {
    use                     generic-service
    host_name               <remote_host_name>
    service_description     PING
    check_command           check_ping!100.0,20%!500.0,60%
}

define service {
    use                     generic-service
    host_name               <remote_host_name>
    service_description     Root Partition
    check_command           check_nrpe!check_disk
}

define service {
    use                     generic-service
    host_name               <remote_host_name>
    service_description     Current Users
    check_command           check_nrpe!check_users
}

define service {
    use                     generic-service
    host_name               <remote_host_name>
    service_description     Total Processes
    check_command           check_nrpe!check_procs
}

define service {
    use                     generic-service
    host_name               <remote_host_name>
    service_description     Load
    check_command           check_nrpe!check_load
}
```

Include the New Configuration in Nagios:  

Edit the main Nagios configuration file to include your new host configuration:  

```bash
sudo nano /usr/local/nagios/etc/nagios.cfg
```

Add the following line:  

```bash
cfg_file=/usr/local/nagios/etc/servers/<remote_host_name>.cfg
```

### 8.3 Define NRPE Commands in Nagios  
You need to define the NRPE commands in the commands configuration file. Usually, this is done in the commands.cfg file.  

### 8.3.1 Open the commands.cfg File
```bash
sudo nano /usr/local/nagios/etc/objects/commands.cfg
```

### 8.3.2 Add the NRPE Command Definitions
Add the following command definitions to the commands.cfg file:

```bash
define command {
    command_name    check_nrpe
    command_line    $USER1$/check_nrpe -H $HOSTADDRESS$ -c $ARG1$
}

define command {
    command_name    check_users
    command_line    $USER1$/check_nrpe -H $HOSTADDRESS$ -c check_users
}

define command {
    command_name    check_load
    command_line    $USER1$/check_nrpe -H $HOSTADDRESS$ -c check_load
}

define command {
    command_name    check_disk
    command_line    $USER1$/check_nrpe -H $HOSTADDRESS$ -c check_disk
}

define command {
    command_name    check_procs
    command_line    $USER1$/check_nrpe -H $HOSTADDRESS$ -c check_procs
}
```

The check_nrpe command is the generic NRPE command used to run a specified command on the remote host.
The other commands (check_users, check_load, etc.) are specific commands to check the number of users, load, disk usage, and processes on the remote host.
### 8.3.3 Save and Exit
Save the file and exit the editor.  

### 8.4 Verify the Configuration  

Before restarting Nagios, verify that your configuration is correct:

```bash
sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
```

### 8.5 Restart Nagios
If the configuration verification passes without errors, restart Nagios:

```bash
sudo systemctl restart nagios
```

### 8.6 Check Nagios Web Interface
Go back to the Nagios web interface at http://<your-server-ip>/nagios. You should now see the Remote Host and the services you configured for monitoring. 

## 9. Checking Logs for Python Application Deployed as a Service

### 9.1 System Logs

When a Python application is deployed as a service, especially using `systemd`, the logs are typically managed by `systemd` and stored in the system journal. To access these logs, you can use the `journalctl` command.

### 9.1.1 Viewing Systemd Service Logs

To view logs specifically for your service, run the following command:

```bash
sudo journalctl -u <your_service_name>.service
```
Replace <your_service_name> with the name of your service file (e.g., myapp if your service file is myapp.service).

Example:
```bash
sudo journalctl -u myapp.service
```

This command will display all logs associated with your Python application service. It includes logs related to the application startup, shutdown, and any messages logged during runtime.  


### 9.1.2 Filtering Logs by Time
To filter logs by a specific time frame, you can use:

```bash
sudo journalctl -u <your_service_name>.service --since "2024-09-20 12:00:00" --until "2024-09-20 14:00:00"
```

This command filters logs between the specified time range.

  
### 9.1.3 Persistent Logs  

If you want to store these logs persistently, ensure that systemd is configured to save logs in /var/log/journal/ by checking /etc/systemd/journald.conf for the Storage=persistent setting.

  
### 9.2 Web Server Logs (Nginx)  

As our Python application is served through Nginx, We can find the relevant logs in the Nginx log files.

### 9.2.1 Access Logs  

Nginx access logs record all requests made to the web server, including those to your Python application.

  
Default Location:
```bash
/var/log/nginx/access.log
```

### 9.2.2 Error Logs
Nginx error logs capture any issues that arise when handling requests, including errors encountered by your Python application.


Default Location:
```bash
/var/log/nginx/error.log
```  
### 9.2.3 Checking Nginx Logs  

To check the most recent log entries:  


Access Log:  

```bash
tail -f /var/log/nginx/access.log
```

Error Log:

```bash
tail -f /var/log/nginx/error.log
```

The -f option allows you to follow the log file in real-time, which is helpful for debugging issues as they occur.

### 9.2.4 Log Rotation
Nginx logs are usually rotated automatically by logrotate, which archives old logs and keeps the log file sizes manageable. You can check the log rotation configuration in /etc/logrotate.d/nginx.

### 9.3. Application-Specific Logs
If your application uses Python's built-in logging module and writes to a custom log file, ensure that the log file is configured properly in your application code.  

Example Configuration:

```python
import logging
logging.basicConfig(filename='/var/log/myapp.log', level=logging.INFO)
logging.info('Application started')
```

Custom Log File Location:  

```bash
/var/log/myapp.log
```
In this example, logs are written to /var/log/myapp.log. You can view these logs with:

```bash
tail -f /var/log/myapp.log
```

## 10. Additional Notes
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
```






