# 🔐 IAM Deep Dive – Interview Focused

---

## 📌 What is IAM?

IAM (Identity and Access Management) allows you to securely control access to AWS services and resources.

It answers 3 main questions:

- Who can access?
- What can they access?
- Under what conditions?

---

## 🧱 Core Components of IAM

### 1️⃣ Users
Represents a person or application that needs access.

### 2️⃣ Groups
Collection of users with shared permissions.

### 3️⃣ Roles
Temporary credentials assigned to AWS services or users.

### 4️⃣ Policies
JSON documents that define permissions.

---

## 🎯 IAM User vs IAM Role (Very Important Interview Question)

| Feature | IAM User | IAM Role |
|----------|----------|----------|
| Long-term credentials | Yes | No |
| Used by humans | Yes | Sometimes |
| Used by AWS services | No | Yes |
| Access keys required | Yes | No |
| Best practice for EC2 | ❌ | ✅ |

✅ In production, we prefer IAM Roles over access keys.

---

## 🔑 Inline Policy vs Managed Policy

### Inline Policy
- Directly attached to one user/role
- One-to-one relationship
- Harder to manage at scale

### Managed Policy
- Reusable
- Can attach to multiple users/roles
- Best practice

---

## 🔄 What is AssumeRole?

AssumeRole allows a user or service to temporarily take permissions of a role.

Used in:
- Cross-account access
- EC2 accessing S3
- Temporary privilege escalation

---

## 🏗 Real Practical Scenario

### 🎯 Requirement:
EC2 instance should access S3 bucket WITHOUT storing access keys.

### ✅ Solution:
1. Create IAM Role
2. Attach S3 Read policy
3. Attach role to EC2 instance
4. Access S3 from EC2 directly

No access key required.

---

## 🔐 Trust Policy vs Permission Policy

### Trust Policy
Defines WHO can assume the role.

Example:
- EC2 service
- Another AWS account

### Permission Policy
Defines WHAT actions are allowed.

Example:
- s3:GetObject
- ec2:DescribeInstances

---

## 🧠 Interview Questions

### Q1: Why should we avoid using access keys in production?

Because:
- They are long-term credentials
- Can leak
- Hard to rotate
- Security risk

IAM Roles provide temporary credentials and are more secure.

---

### Q2: How does EC2 access S3 without credentials?

Using:
IAM Role attached to EC2 instance.

AWS automatically provides temporary credentials via metadata service.

---

### Q3: Difference between Security Group and IAM?

| Security Group | IAM |
|---------------|------|
| Network level | Identity level |
| Controls traffic | Controls permissions |
| Works at EC2/VPC level | Works at user/service level |

---

## 🚨 Common Mistakes in Production

- Using root account for daily work
- Hardcoding credentials in code
- Giving AdministratorAccess to everyone
- Not enabling MFA
- Not rotating access keys

---

## ✅ Best Practices

- Use IAM Roles instead of access keys
- Enable MFA for all users
- Follow Least Privilege Principle
- Use Managed Policies
- Enable CloudTrail logging
- Avoid using root account

---

## 🎯 Real Interview Tip

When interviewer asks:

"How would you securely allow EC2 to access S3?"

Answer confidently:

"I would create an IAM role with required S3 permissions, attach it to the EC2 instance, and avoid storing any static access keys. This follows least privilege and improves security posture."

---

# 🔥 Summary

IAM controls:
- Authentication
- Authorization
- Access delegation
- Cross-account access
- Secure production design

Mastering IAM is critical for clearing AWS/DevOps interviews.
# 🔐 IAM Deep Dive – Enterprise Level

---

# 🟢 हिन्दी

IAM AWS का heart है।

## Key Components

- Users
- Groups
- Roles
- Policies

---

## 🛡️ Enterprise Best Practices

1. Least Privilege
2. Role-based access
3. MFA enforcement
4. Password policy strict
5. No root usage
6. Use IAM Roles for EC2
7. Cross-account access via role assumption

---

## 🔎 Policy Types

- Managed Policies
- Inline Policies
- Resource-based Policies

---

## 🔥 Real Scenario

Production EC2 had S3 full access.

Action:

Created custom policy:
Only GetObject access to specific bucket.

Result:

Reduced blast radius risk.

---

# 🔵 English Summary

IAM strategy in enterprise:

- Enforce least privilege
- Use IAM roles instead of users
- Enable MFA
- Monitor using CloudTrail
- Rotate credentials

---

# 📚 Official Reference

IAM Best Practices:
https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html