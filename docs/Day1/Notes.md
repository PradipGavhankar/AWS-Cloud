# 🚀 Day 1 – AWS EC2 Introduction

---

## 1️⃣ AWS Console Overview

Screenshot:

![AWS Console](../../images/Day1/01-ec2-dashboard.png)

---

## 2️⃣ EC2 Instance List

Screenshot:

![EC2 Instance List](../../images/Day1/02-launch-instance.png)

### Key Observations:

- Instance ID
- Instance Type (t2.micro)
- Availability Zone
- Instance State
- Status Checks
- Public DNS

---

## 3️⃣ Instance Running

![Instance Running](../../images/Day1/03-instance-running.png)

---

## 4️⃣ Instance Details

![Instance Details](../../images/Day1/04-instance-details.png)
---

# 🚀 Day 1 – AWS EC2 Introduction & SSH Access

---

## 🖥️ AWS Console Overview

### 🟢 Hindi Explanation

AWS Console ek web-based dashboard hai jahan se hum EC2, S3, IAM jaise services manage karte hain.

EC2 dashboard mein:
- Instances dekh sakte hain
- New instance launch kar sakte hain
- Instance status monitor kar sakte hain

### 🔵 English Explanation

AWS Console is a web interface to manage AWS services.

In EC2 Dashboard we can:
- View instances
- Launch instances
- Monitor instance health

---

## 📋 EC2 Instance Information

EC2 Instance list mein important cheezein:

- Instance ID
- Instance Type (t2.micro)
- Availability Zone
- Instance State (Running / Stopped)
- Status Checks (2/2 passed)
- Public IP
- Private IP
- Security Group

---

## 🟢 Instance Running State

Jab instance **Running** show kare aur **2/2 Status Checks passed** ho,
tab server ready hai use karne ke liye.

---

# 🔐 Connecting to EC2 using SSH

---

## 🟢 Hindi Explanation

EC2 server mein login karne ke liye chahiye:

- Public IP address
- .pem key file
- Security group mein Port 22 open hona chahiye

SSH (Secure Shell) ek secure encrypted connection provide karta hai.

---

## 🔵 English Explanation

To connect to EC2 securely, we need:

- Public IP
- Private key (.pem file)
- Port 22 open in Security Group

SSH provides encrypted remote access to the Linux server.

---

## 🧱 SSH Commands

```bash
# Step 1: Key permission secure karo
chmod 400 day1-key.pem

# Step 2: SSH login karo
ssh -i day1-key.pem ec2-user@13.233.45.120
```

---

## 🚀 Real Output Example

```bash
The authenticity of host '13.233.45.120' can't be established.
Are you sure you want to continue connecting (yes/no)? yes

Warning: Permanently added '13.233.45.120' to the list of known hosts.

       __|  __|_  )
       _|  (     /   Amazon Linux 2 AMI
      ___|\___|___|

[ec2-user@ip-172-31-25-10 ~]$
```

Agar yeh prompt aa gaya:

```
[ec2-user@ip-172-31-25-10 ~]$
```

Toh 🎉 SSH successful hai.

---

# ✅ Good Practices (Production Mindset)

- SSH access sirf apne IP tak restrict karo (My IP)
- .pem file kabhi GitHub ya public repo mein upload mat karo
- Production mein Bastion Host use karo
- Root login disable rakho
- Minimum required ports hi open karo (Principle of Least Privilege)
- IAM roles use karo instead of storing credentials
- Monitoring & logging enable rakho

---

# ❌ Bad Practices (Danger Zone)

- Port 22 ko 0.0.0.0/0 se open kar dena
- Private key WhatsApp ya email se share karna
- Root user se direct kaam karna
- Production changes bina documentation ke karna
- Manual changes karna bina Infrastructure as Code use kiye
- Credentials code ke andar hardcode karna

---

# 🧠 Interview Ready Question

**Q: Why should we not allow SSH from 0.0.0.0/0 in production?**

**Answer:**
Because it exposes the server to the entire internet, increasing the risk of brute-force attacks and unauthorized access.

---

# 🎯 Day 1 Summary

✔ EC2 Launch  
✔ Instance Monitoring  
✔ Public & Private IP Understanding  
✔ SSH Connection  
✔ Security Best Practices  
✔ Production Mindset  

---
