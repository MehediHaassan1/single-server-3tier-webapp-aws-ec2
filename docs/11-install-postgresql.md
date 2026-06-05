## 📄 PostgreSQL Install & Configuration (Ubuntu EC2)

### 1. Install PostgreSQL

```
sudo apt update
sudo apt install postgresql postgresql-contrib -y
```

### 2. Check service status

```
sudo systemctl status postgresql
```

### Enable & Start service (if not active)

```
sudo systemctl enable postgresql
sudo systemctl start postgresql
```

### 3. Login to postgres user

```
sudo -i -u postgres
psql
```

### 4. Set password for postgres user

```
ALTER USER postgres PASSWORD 'your_strong_password';
```

### 5. Create database

```
CREATE DATABASE appdb;
```

### 6. Create application user (BEST PRACTICE)

```
CREATE USER appuser WITH PASSWORD 'app_password';
```

### 7. Grant privileges

```
GRANT ALL PRIVILEGES ON DATABASE appdb TO appuser;
```

### 8. Exit PostgreSQL

```
exit
```

### 9. Login again with password (optional test)

```
psql -U postgres -h localhost -W
```

#### or app user:

```
psql -U appuser -d appdb -h localhost -W
```

### 10. Navigate into database (VERY IMPORTANT)

```
sudo -i -u postgres
psql
```

#### Then:

```
\c appdb
```

### !Now here you can run your sql query.

### Best practices (important)

- ✔ Always use appuser (not postgres)
- ✔ Never expose port 5432 publicly
- ✔ Use .env for credentials
- ✔ Keep DB inside private network

### Final summary

Install → Configure → Create DB → Create user → Navigate DB

```
psql → ALTER USER → CREATE DATABASE → CREATE USER → GRANT → \c appdb
```
