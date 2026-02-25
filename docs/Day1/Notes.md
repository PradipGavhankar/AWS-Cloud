# Day 1 – AWS EC2 Introduction

---

## 1️⃣ AWS Console Overview

Screenshot:
![AWS Console](../../images/Day1/aws-console-dashboard.png)

---

## 2️⃣ EC2 Instance List

Screenshot:
![EC2 Instance List](../../images/Day1/ec2-instance-list.png)

Key Observations:
- Instance ID
- Instance Type (t2.micro)
- Availability Zone
- Instance State
- Status Checks
- Public DNS

---

## 3️⃣ EC2 Instance Details

Screenshot:
![EC2 Instance Details](../../images/Day1/ec2-instance-details.png)

Important Fields:
- Public IP
- Private IP
- Public DNS
- Instance State
- Security Group

---

## 4️⃣ Security Groups

Screenshot:
![Security Group](../../images/Day1/security-group-config.png)

Security Group works as:
- Virtual Firewall
- Controls inbound and outbound traffic

---

## 📌 Key Learnings

- EC2 is Infrastructure as a Service (IaaS)
- Public IP changes on stop/start (unless Elastic IP attached)
- Security Group is stateful
- Always document infra changes

---

## 🚀 Next Steps

- Launch EC2 using CLI
- Attach Elastic IP
- Practice key pairs
- Understand IAM roles