
## 📝 Overview
Setup a **secure VPC** with public & private subnets, routing, and security groups to host applications safely.

---

## 🛠️ Features
- Custom VPC: `10.0.0.0/16`  
- Public & Private Subnets  
- Internet Gateway (IGW) & NAT Gateway  
- Security Groups for controlled access  
- EC2 instance in public subnet  

---

## 🌐 Architecture
Internet → IGW → Public Subnet → EC2 (SSH 22, HTTP 80/8080)  
                     ↓  
                 Private Subnet → Private Resources → NAT

---

## ⚡ Setup Steps
1. **Create VPC**: `secure-vpc`, CIDR `10.0.0.0/16`, enable DNS  
2. **Create Subnets**: Public `10.0.1.0/24`, Private `10.0.2.0/24`  
3. **Attach IGW**: Route `0.0.0.0/0` from public subnet  
4. **Deploy NAT**: Route `0.0.0.0/0` from private subnet  
5. **Security Groups**: Public → SSH(22), HTTP(80/8080); Private → internal only  
6. **Launch EC2**: In public subnet, assign public IP, connect via SSH

---

## 🔑 Key Concepts
- **IP/Subnet** → Network segmentation  
- **Ports** → 22 (SSH), 80/8080 (Web)  
- **Security Groups** → Firewall rules  
- **NAT Gateway** → Internet access for private subnet  

---

## 🚀 Outcome
- Secure VPC with public & private subnets  
- EC2 instance running in public subnet  
- Ready for secure app deployment  

---
