# 💰 AWS Production Cost Modelling (FinOps Perspective)

---

# 🟢 हिन्दी – AWS में Resources कहाँ Create होते हैं?

AWS में resources logical layers में create होते हैं:

## 🏗️ 1. Networking Layer
- VPC
- Public / Private Subnet
- Internet Gateway
- NAT Gateway
- Route Tables
- Security Groups

## 💻 2. Compute Layer
- EC2 Instances
- Auto Scaling Groups
- Load Balancer (ALB/NLB)
- EKS Cluster
- Lambda

## 🗄️ 3. Storage Layer
- EBS
- S3
- EFS

## 🛢️ 4. Database Layer
- RDS
- DynamoDB
- Aurora

## 📊 5. Monitoring & Governance
- CloudWatch
- CloudTrail
- AWS Budgets
- Config

---

# 🔵 English – Production Architecture Cost Scenario

Assume small production setup:

- 3 EC2 (t3.medium)
- 1 Application Load Balancer
- 1 NAT Gateway
- 1 RDS db.t3.medium
- 500GB S3 Storage
- 300GB EBS Storage
- EKS Cluster (Control Plane)
- 2TB Data Transfer per month

Region: US-East (Approximate Pricing)

---

# 📊 Cost Comparison Table

| Service | Monthly ($) | Yearly ($) | 3 Years ($) |
|----------|-------------|------------|-------------|
| EC2 (3 x t3.medium) | 90 | 1080 | 3240 |
| RDS | 80 | 960 | 2880 |
| ALB | 25 | 300 | 900 |
| NAT Gateway | 35 | 420 | 1260 |
| EKS Control Plane | 73 | 876 | 2628 |
| EBS (300GB) | 30 | 360 | 1080 |
| S3 (500GB) | 12 | 144 | 432 |
| Data Transfer (2TB) | 180 | 2160 | 6480 |
| Monitoring & Misc | 20 | 240 | 720 |
| **Total** | **545** | **6540** | **19620** |

---

# 💡 Cost Optimization Scenario

If we apply:

- Savings Plan (30% compute discount)
- Rightsizing unused EC2
- Stop non-prod servers at night
- S3 lifecycle policy
- Remove unused Elastic IP

New Estimated Monthly Cost ≈ $480  
Yearly ≈ $5760  
3 Years ≈ $17280  

### 🎯 3-Year Savings:
19620 - 17280 = **$2340 saved**

---

# 🏆 Interview Explanation (हिन्दी)

"इस architecture का monthly खर्च लगभग $545 है।  
अगर Savings Plan और proper rightsizing करें तो 3 साल में लगभग $2300 की बचत हो सकती है।  
मैं हमेशा cost को monthly, yearly और 3-year view में analyse करता हूँ क्योंकि management long-term budgeting देखती है।"

---

# 🏆 Interview Explanation (English)

"This architecture costs approximately $545 per month.  
Over 3 years, it reaches nearly $19,620.  
By applying Savings Plans and optimization strategies, we can reduce around $2,300 in 3 years."

---

# 📚 Official References

AWS Pricing Calculator:
https://calculator.aws/

AWS EC2 Pricing:
https://aws.amazon.com/ec2/pricing/

AWS RDS Pricing:
https://aws.amazon.com/rds/pricing/

AWS EKS Pricing:
https://aws.amazon.com/eks/pricing/

AWS Savings Plans:
https://aws.amazon.com/savingsplans/

---

# 😊 Final Thought

Cloud खर्च control करना cost cutting नहीं है,  
यह intelligent architecture design है.