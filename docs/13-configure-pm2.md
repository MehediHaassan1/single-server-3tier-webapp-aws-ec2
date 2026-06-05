# 🚀 Configure PM2

## 1. Install PM2

Install PM2 globally:

```bash
sudo npm install -g pm2
```

Verify installation:

```bash
pm2 --version
```

---

## 2. Start the Application

Navigate to the backend directory:

```bash
cd /path/to/backend
```

Start the application with PM2:

```bash
pm2 start dist/server.js --name test-app-backend
```

> Replace `dist/server.js` with your application's entry file if different.

---

## 3. Verify Application Status

```bash
pm2 status
```

Expected output:

```text
┌────┬──────────────────┬────────┬─────┐
│ id │ name             │ status │ cpu │
├────┼──────────────────┼────────┼─────┤
│ 0  │ test-app-backend │ online │ 0%  │
└────┴──────────────────┴────────┴─────┘
```

---

## 4. View Application Logs

```bash
pm2 logs test-app-backend
```

View the last 100 log lines:

```bash
pm2 logs test-app-backend --lines 100
```

---

## 5. Restart the Application

```bash
pm2 restart test-app-backend
```

---

## 6. Stop the Application

```bash
pm2 stop test-app-backend
```

---

## 7. Delete the Application

```bash
pm2 delete test-app-backend
```

---

## 8. Enable Auto Start on Server Reboot

Generate startup configuration:

```bash
pm2 startup
```

PM2 will output a command similar to:

```bash
sudo env PATH=$PATH:/usr/bin pm2 startup systemd -u ubuntu --hp /home/ubuntu
```

Run the generated command.

Save the current PM2 process list:

```bash
pm2 save
```

---

## 9. Verify Saved Processes

```bash
pm2 list
pm2 save
```

After a server reboot, PM2 will automatically restore all saved applications.

---

## Useful Commands

### Show application details

```bash
pm2 show test-app-backend
```

### Monitor CPU and memory usage

```bash
pm2 monit
```

### Reload application with zero downtime

```bash
pm2 reload test-app-backend
```

### View all running applications

```bash
pm2 list
```

---

## Deployment Flow

```text
Backend Application
        │
        ▼
      PM2
        │
        ▼
 Automatic Restart
        │
        ▼
 Server Reboot Recovery
```