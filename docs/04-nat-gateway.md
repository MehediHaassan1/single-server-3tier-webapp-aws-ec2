# NAT Gateway Setup

## 1. What is NAT Gateway?
NAT Gateway allows instances in a private subnet to access the internet without exposing them publicly.

It works only for outbound traffic.

---

## 2. Why NAT Gateway is needed?
- Private subnet resources cannot directly access internet
- But they may need internet for updates, packages, APIs
- NAT provides secure outbound internet access

---

## 3. What I created

- NAT Gateway: `single-server-nat-gw`
- Elastic IP attached
- Placed in Public Subnet

---

## 4. How it works

Private subnet traffic goes like this:

Private Subnet → NAT Gateway → Internet Gateway → Internet

---

## 5. Key Point

NAT Gateway only allows:
- OUTBOUND traffic (private → internet)
- BLOCKS inbound traffic (internet → private)