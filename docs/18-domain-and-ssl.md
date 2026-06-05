## 1: Request SSL Certificate (ACM)
### Request Certificate
- Request a public certificate
- Domain name:
```
example.com
www.example.com
```
- Validation Method:
```
DNS Validation
```
AWS recommends DNS validation and can automatically validate through Route 53.

## 2: Validate Certificate
Create records in Route 53

AWS automatically creates the validation CNAME records. After a few minutes the certificate status should become:
```
Issued
```

## 3: Add HTTPS Listener to ALB
Go to:

EC2 → Load Balancers → single-server-alb

**Listeners**

Add Listener:
```
HTTPS : 443
```
Select:

- Forward to signle-server-tg
- Choose the ACM certificate you created.

AWS ALB supports ACM certificates directly.

## 4: Redirect HTTP to HTTPS

**Edit Listener:**

HTTP : 80

**Instead of:**

Forward to Target Group

Change to:

- Redirect to HTTPS
- Port: 443
- Status code: HTTP_301

Result:
```TEXT
http://example.com
        ↓
https://example.com
```

## 5: Create DNS Record
### If Using Route 53
Hosted Zone → Your Domain

Create Record:

### Root Domain
```TEXT
Type: A
Alias: Yes
Alias Target:
single-server-alb-xxxxx.ap-south-1.elb.amazonaws.com
```

### Subdomain
```TEXT
Type: A
Alias: Yes
Alias Target:
same ALB
```

For ALBs, Route 53 Alias records should point directly to the ALB instead of using fixed IPs.

## 6: Security Group
ALB Security Group:
```
HTTP 80  → 0.0.0.0/0
HTTPS 443 → 0.0.0.0/0
```
EC2 Security Group:
```
HTTP 80 → ALB Security Group
```

No public access to EC2 required.

## Verify

After DNS propagation:
```
https://yourdomain.com
```
You should see:

- ✅ SSL lock icon

- ✅ HTTPS connection

- ✅ ALB handling traffic

- ✅ Private EC2 serving application