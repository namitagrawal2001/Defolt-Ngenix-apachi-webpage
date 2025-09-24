# Static Website Deployment on Linux (Nginx + Apache)

## Project Overview
This is a basic static website deployed on a Linux server using **Nginx** and **Apache**.  
It demonstrates how to host static files, configure ports, and optionally enable HTTPS with a self-signed certificate (for IP-based access).

### Website Features
- Static HTML, CSS, and JavaScript
- Nginx serving on port 80
- Apache serving on port 8080
- Basic styling and a button with JavaScript alert

---

## Folder Structure

website/
├── index.html
├── style.css
└── script.js


---

## Setup & Deployment Steps

### 1. Connect to Server
```bash
ssh -i "your-key.pem" ubuntu@your_server_ip

#Update System and Install packages
sudo apt update
sudo apt install nginx apache2 git -y


#Prepare Website Folder
mkdir ~/website


Place your files: index.html, style.css, script.js.

#Configure Nginx
sudo cp -r ~/website/* /var/www/html/
sudo systemctl restart nginx
sudo systemctl enable nginx


Access via: http://your_server_ip



#Configure Apache on Port 8080
sudo nano /etc/apache2/ports.conf  # Change Listen 80 to Listen 8080
sudo nano /etc/apache2/sites-available/000-default.conf  # Change <VirtualHost *:80> to <VirtualHost *:8080>
sudo cp -r ~/website/* /var/www/html/
sudo systemctl restart apache2
sudo systemctl enable apache2

#Restart Nginx:

sudo nginx -t
sudo systemctl restart nginx


Access via: https://your_server_ip (browser may show warning due to self-signed certificate)
