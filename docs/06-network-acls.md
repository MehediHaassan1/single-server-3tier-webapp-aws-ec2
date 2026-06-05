# Network ACL (NACL) Setup

## 1. What is NACL?

Network ACL is a stateless firewall at subnet level that controls inbound and outbound traffic.

---

## 2. Why NACL is used?

- Extra security layer on subnet
- Control traffic at network level
- Works before Security Groups

---

## 3. What I used

- Default NACL or custom NACL (based on setup)
- Associated with public and private subnets

---

## 4. How it works

Each rule is evaluated in order:

Inbound Rules → Subnet → Outbound Rules

---

## 5. NACL vs Security Group

| Feature | NACL         | Security Group |
| ------- | ------------ | -------------- |
| Level   | Subnet       | Instance       |
| Type    | Stateless    | Stateful       |
| Rules   | Allow & Deny | Allow only     |

---

## 6. Key Understanding

- NACL works at subnet level
- Security Group works at instance level
- Both together provide layered security
