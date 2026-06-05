# 🚀 Configure Nginx Reverse Proxy

## 1. Check Nginx Status

```bash
sudo systemctl status nginx
```

### If Nginx is active

You should see:
```
active (running)
```
Proceed to the next step.

## If Nginx is not installed
### Install Nginx:
```
sudo apt update
sudo apt install nginx -y
```

### Enable and start the service:
```
sudo systemctl enable nginx
sudo systemctl start nginx
```

## If Nginx is installed but not running

### Start the service:
```
sudo systemctl start nginx
```

### Verify:
```
sudo systemctl status nginx
```

## If Nginx fails to start
### Check the error logs:
```
sudo journalctl -u nginx -n 50 --no-pager
```

### Validate the Nginx configuration:
```
sudo nginx -t
```

### Fix any reported errors and restart:
```
sudo systemctl restart nginx
```

### Confirm Nginx is enabled on boot
```
sudo systemctl enable nginx
```

## Now Copy Build Files
Create a directory for the frontend:

```bash
sudo mkdir -p /var/www/frontend
```

Copy the build files:
```bash
sudo cp -r dist/* /var/www/frontend/
```

Set proper permissions:

```bash
sudo chown -R www-data:www-data /var/www/frontend
sudo chmod -R 755 /var/www/frontend
```

## Configure Nginx

Open the default Nginx configuration:

```bash
sudo nano /etc/nginx/sites-available/default
```

Replace the existing configuration with:

```nginx
server {
    listen 80;
    server_name _;

    root /var/www/frontend;
    index index.html;

    # Frontend
    location / {
        try_files $uri $uri/ /index.html;
    }

    # Backend API
    location /api/ {
        proxy_pass http://localhost:5000;

        proxy_http_version 1.1;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```
> Replace `5000` with your backend application's port if different.

## Test Nginx Configuration

```bash
sudo nginx -t
```

Expected output:

```text
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

## Restart Nginx

```bash
sudo systemctl restart nginx
```

Verify the service status:

```bash
sudo systemctl status nginx
```

---

## Request Flow

```text
Browser
   │
   ▼
Nginx (Port 80)
   │
   ├── /        → Frontend (/var/www/frontend)
   │
   └── /api/*  → Backend (localhost:5000)
```

## Security Recommendations

- Run the backend on `localhost` only.
- Do not expose the backend port in the EC2 Security Group.
- Allow only:
  - Port 80 (HTTP)
  - Port 443 (HTTPS)
  - Port 22 (SSH, restricted as needed)