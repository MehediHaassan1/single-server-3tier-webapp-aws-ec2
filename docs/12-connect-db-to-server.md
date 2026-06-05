# Connect PostgreSQL Database to Node.js Server

## 🧠 Overview

This document explains how to connect a Node.js backend server with a PostgreSQL database using a connection pool.

---

## ⚙️ 1. Install Required Package

We use the `pg` library to connect Node.js with PostgreSQL.

```bash
npm install pg
```

## 2. Environment Variables Setup

```
DATABASE_URL=postgresql://appuser:app_password@localhost:5432/appdb
PORT=3000
NODE_ENV=development
```

`Or adjust any additional configuration as needed.`

## 3. Test Connection

### Run server

```
npm run dev
```

## Architecture Flow

Client Request  
↓  
Express Server (Node.js)  
↓  
Connection Pool (pg)  
↓  
PostgreSQL Database (appdb)

## Key Points
- Uses connection pooling for performance
- Uses .env for secure credentials
- Supports scalable database connections
- Safe production-ready structure