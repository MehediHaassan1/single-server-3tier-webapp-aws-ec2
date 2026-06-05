# Connecting to EC2 Instance (Various Methods)

## Overview
There are multiple ways to connect to an AWS EC2 instance depending on architecture, security design, and network configuration.

In this project, the EC2 instance is deployed in a private subnet, so secure access is handled primarily through AWS Systems Manager (SSM).

---

## Method 1: AWS Systems Manager (SSM) — Recommended

### What is it?
AWS Systems Manager (SSM) allows secure access to EC2 instances without using SSH or opening port 22.

### Why I used it?
- No public IP required
- No SSH key exposure over internet
- IAM-based access control
- Production-grade secure approach

### Requirements:
- SSM Agent installed (default in AWS Ubuntu AMIs)
- IAM role attached to EC2 with SSM permissions
- NAT Gateway for outbound internet access (for private subnet)

---

## Method 2: SSH (Key-based Access)

### What is it?
Traditional method using a PEM key file to access EC2 via SSH.

### Command:
```bash
ssh -i key.pem ubuntu@<public-ip>
```

### Requirements:
- EC2 must have a public IP
- Security Group must allow port 22
- PEM key must be securely stored

### Notes:
- Not used in this project due to security design
- Exposes instance if misconfigured

## Method 3: EC2 Instance Connect (Browser-based SSH)

### What is it?
AWS provides browser-based SSH access directly from the AWS Console.

### How it works:
- Connect directly from AWS Management Console
- Temporary SSH session is created

### Limitations:
- Works only for instances with public IP
- Requires port 22 open in Security Group
- Not suitable for private subnet architecture

## Method 4: Session Manager (AWS CLI)

### What is it?
A feature of AWS SSM that allows terminal access via AWS CLI.

```
aws ssm start-session --target <instance-id>
```

### Requirements:
- AWS CLI configured
- IAM role with SSM permissions
- SSM agent running on EC2

### Benefits:
- No SSH required
- Fully logged and auditable
- Works in private subnet