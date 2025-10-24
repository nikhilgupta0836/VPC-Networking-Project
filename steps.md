
## 1. Design & Configure the VPC
- Create a new VPC  
  - Name: `secure-vpc`  
  - CIDR Block: `10.0.0.0/16`  
  - Enable DNS hostnames and DNS resolution  
- Create two subnets in that VPC  
  - Public Subnet: `10.0.1.0/24` (Enable “Auto-assign public IP”)  
  - Private Subnet: `10.0.2.0/24` (Do not assign a public IP)  

## 2. Setup Internet Gateway & NAT Gateway
- Create an Internet Gateway (IGW)  
  - Name: `secure-igw`  
  - Attach it to `secure-vpc`  
- Allocate an Elastic IP and create a NAT Gateway in the **Public Subnet**  
  - Name: `secure-nat-gw`  
  - Associate the Elastic IP  

## 3. Configure Route Tables
- Public Route Table  
  - Name: `public-rt`  
  - Associate with the Public Subnet  
  - Add route: `0.0.0.0/0 → Internet Gateway (IGW)`  
- Private Route Table  
  - Name: `private-rt`  
  - Associate with the Private Subnet  
  - Add route: `0.0.0.0/0 → NAT Gateway`  

## 4. Launch EC2 Instances & Secure Access
- Launch an EC2 instance in **Public Subnet**  
  - AMI: Amazon Linux 2  
  - Assign a public IP  
  - Name: `public-ec2`  
  - Security Group: `public-sg`  
    - Inbound: SSH (22), HTTP (80)  
    - Outbound: All  
- Launch an EC2 instance in **Private Subnet**  
  - Name: `private-ec2`  
  - No public IP  
  - Security Group: `private-sg`  
    - Inbound: SSH (22) only from Public Subnet CIDR  
    - Outbound: All  

## 5. Configure Security Groups & Network ACLs
- **public-sg**  
  - Inbound: SSH (22), HTTP (80) from Internet  
  - Outbound: All  
- **private-sg**  
  - Inbound: SSH (22) from Public Subnet  
  - Outbound: All  

## 6. Validation & Testing
- SSH into `public-ec2`:  
  ```bash
  ssh -i <your-key>.pem ec2-user@<Public-EC2-Public-IP>
