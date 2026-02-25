# ☁ AWS Cloud Learning Journey

This repository documents my structured AWS learning path including:

- Core AWS Services
- EC2 & Compute
- Networking
- Cost Optimization
- Terraform
- Monitoring & Governance
- Real-world Scenarios
- Production Best Practices

---

## 📂 Repository Structure


---

## 🚀 Day 1 – EC2 Introduction

Topics Covered:

- What is EC2
- Launching EC2 Instance
- Instance States
- Public IP & Public DNS
- Security Groups

Detailed notes available at:


---

## 🎯 Goal

Build strong AWS fundamentals with production-ready best practices and proper documentation.

---

## 🔥 Best Practices Followed

- Version control enabled
- No manual portal changes without documentation
- Clean folder structure
- Image documentation for every practical

---

### 📌 Author
Pradip – DevOps & Cloud Learning Journey


Format rahega:
🟢 पहले हिन्दी में आसान समझ
🔵 फिर English explanation
🧱 फिर simple code (Hindi comments)
✅ Good Practice
❌ Bad Practice
😂 Thoda DevOps comedy
🚀 Real output example
✅ Good Practice (Production Ready Mindset)
✔ Always use version constraint
✔ Variables use करो hardcoding मत करो
✔ State file Git में commit मत करो
✔ terraform plan production में mandatory
✔ Use remote backend (later section)
❌ Bad Practice (Danger Zone)
❌ Hardcoded subscription ID
❌ State file GitHub में push करना
❌ Direct apply in production
❌ No version control
❌ Portal से manually change करना


# Check existing remote
git remote -v

# Remove wrong remote (forcefully)
git remote remove origin

# Add correct remote
git remote add origin https://github.com/PradipGavhankar/AWS-Cloud.git

# Push to GitHub
git push -u origin main

git add .
git commit -m "AWS FinOps structure"
git push