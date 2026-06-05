# Security Groups Configuration

## 1. What is Security Group?

A Security Group acts as a virtual firewall for EC2 instances, controlling inbound and outbound traffic at the instance level.

---

## 2. Why Security Groups are used?

- Control access to EC2 instances
- Allow only required ports
- Improve security by minimizing exposure

---

## 3. What I configured

In this project, I created a Security Group for the EC2 instance with minimal required access.

### Inbound Rules

- HTTP (80)
  - Source: 0.0.0.0/0
  - Purpose: Web traffic access

- HTTPS (443)
  - Source: 0.0.0.0/0
  - Purpose: Secure web traffic

### Note:

- SSH (22) is NOT enabled
- Instead, AWS Systems Manager (SSM) is used for instance access

---

## 4. Why I used SSM instead of SSH?

- No need to expose port 22 to the internet
- More secure access method
- Managed by AWS
- No key management required for login

---

## 5. Key Insight

This setup follows a production-like security approach:

- Only web ports are exposed (80, 443)
- Administrative access is handled via SSM
- Reduces attack surface significantly
