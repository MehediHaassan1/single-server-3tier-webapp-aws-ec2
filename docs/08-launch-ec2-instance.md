# Launch EC2 Instance

## 1. What is EC2?

Amazon EC2 (Elastic Compute Cloud) is a virtual server in AWS used to run applications in the cloud.

---

## 2. Why EC2 is used?

- Host backend application
- Run services like Node.js, Nginx
- Provide scalable compute environment

---

## 3. What I created

In this project, I launched an EC2 instance with the following configuration:

### Instance Details

- OS: Ubuntu 26
- Instance Type: t2.micro (or based on selection)
- Network: Custom VPC
- Subnet: Private Subnet
- Security Group: Web Security Group

---

## 4. Key Configuration

### Networking

- Deployed inside a Private Subnet
- No direct public IP exposure

### Access Method

- AWS Systems Manager (SSM) used for secure access
- No SSH port (22) exposed to internet

### Key Pair

- A PEM key was generated and associated with the instance
- Used for initial setup / fallback access if needed

---

## 5. Why Private Subnet?

- EC2 is not directly exposed to internet
- Access is controlled via SSM
- More secure production-like architecture

---

## 6. How it works

User/Admin access flow:

AWS Console / SSM → IAM Role → EC2 Instance (Private Subnet)

---

## 7. Key Insight

This setup follows a secure AWS architecture pattern:

- Private subnet deployment
- No public SSH access
- SSM-based instance management
- Reduced attack surface
