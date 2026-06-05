# 📄 Install Nginx & Basic Setup (Ubuntu EC2)

## Overview

Nginx is a high-performance web server used to serve frontend applications and act as a reverse proxy for backend services.

## 1. Install Nginx

```
sudo apt update
sudo apt install nginx -y
```

## 2. Check Nginx Status

```
sudo systemctl status nginx
```

## 3. Start & Enable Nginx

```
sudo systemctl start nginx
sudo systemctl enable nginx
```

## 4. Test Nginx

Open browser:

```
http://<EC2-PUBLIC-IP>
```

`You should see: “Welcome to nginx”`

## 5. Basic Nginx Structure

Default root directory: /var/www/html

Config file: /etc/nginx/sites-available/default

Logs: /var/log/nginx/

## 6. Basic Nginx Configuration

```
sudo nano /etc/nginx/sites-available/default
```

## Default basic server block

```
server {
    listen 80;
    server_name _;

    root /var/www/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

## 7. Restart Nginx

```
sudo systemctl restart nginx
```

## 8. Test Configuration

```
sudo nginx -t
```

## 9. Important Notes

- Nginx runs on port 80 by default
- Root directory serves static files
- Config file controls routing behavior
- Always restart after changes

## In your full-stack

## Nginx will:

- ✔ Serve React frontend (build files)
- ✔ Proxy /api requests to Node.js backend

## Architecture Flow

Client  
↓  
Nginx (Port 80)  
↓  
Frontend (Static Files) OR Backend (/api proxy)
