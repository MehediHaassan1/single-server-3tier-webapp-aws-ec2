# Target Group & ALB Setup (AWS)

## Overview

A Target Group in AWS Application Load Balancer (ALB) is used to route incoming traffic to one or more registered targets (EC2 instances, IPs, or Lambda functions).

In this project, the architecture is:
```TEXT
Internet
   ↓
Application Load Balancer (ALB)
   ↓
Target Group
   ↓
EC2 Instance (Nginx + Node.js)
```

## 1. Create Application Load Balancer (ALB)

Go to AWS Console:

`EC2 → Load Balancers → Create Load Balancer`

`Step 1:` Choose Load Balancer Type

Select: **Application Load Balancer (ALB)

`Step 2:` Basic Configuration

```
Name: single-server-alb
Scheme: Internet-facing
IP type: IPv4
```

`Step 3:` Network Mapping
- Select your VPC
- Select at least 2 public subnets (different AZs)

`Step 4:` Security Group (ALB SG)

Create or select a security group for ALB:

Inbound rules:
- HTTP 80  → 0.0.0.0/0
- HTTPS 443 → 0.0.0.0/0 (optional)

`Step 5:` Listener

Default listener:
- HTTP : 80

- Forward to Target Group (can attach later)

`Step 6:` Create Load Balancer

Click:

Create Load Balancer

After creation, you will get DNS:

```single-server-alb-xxxx.ap-south-1.elb.amazonaws.com```

## 2. Create Target Group

Go to:

```EC2 → Target Groups → Create Target Group```

### Configuration:
```Target type: Instance
Protocol: HTTP
Port: 80
VPC: Select your custom VPC
```
## 3. Health Check Configuration
```
Protocol: HTTP
Path: /
Port: traffic port (80)
Healthy threshold: 3
Unhealthy threshold: 2
Timeout: 5 seconds
Interval: 30 seconds
```
`Ensure Nginx responds on /`

## 4. Register Targets

Add EC2 instance:

- Select your EC2 instance
- Port: 80
- Click Include as pending below
- Click Register targets

## 5. Target Health Status

After setup, status should be:

healthy ✅

If not healthy, check:

- Nginx is running
- Port 80 is open in EC2 security group
- Correct VPC selected

## 6. Attach Target Group to ALB

Go to:


`EC2 → Load Balancers → Your ALB → Listeners`

Add rule:

- HTTP : 80 → Forward to Target Group

## 7. Traffic Flow
```TEXT
Internet
   ↓
Application Load Balancer (ALB)
   ↓
Target Group
   ↓
EC2 Instance (Nginx + Node.js)
```

## 8. Important Notes
- ALB is the public entry point
- Target Group routes traffic to EC2
- EC2 should NOT be publicly exposed
- Health checks must pass for routing
- Only healthy targets receive traffic

## 9. Common Issues
❌ Target unhealthy
- Nginx not running
- Wrong port (must be 80)
- Security group blocking ALB → EC2 traffic

❌ Timeout error
- No registered targets
- ALB not attached to target group
- Security group misconfiguration

## Summary
- ALB handles incoming internet traffic
- Target Group routes requests to EC2
- Health checks ensure instance availability
- This is a production-grade AWS architecture setup