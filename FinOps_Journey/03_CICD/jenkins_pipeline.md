# 🚀 Jenkins CI/CD Production Pipeline

---

# 🟢 हिन्दी – Pipeline Flow

Flow:

Developer → GitHub → Webhook → Jenkins → Build → Docker → ECR → EKS Deploy

---

## 🛠️ Stages

1. Code Checkout
2. Build (Maven / NPM)
3. Unit Test
4. Docker Build
5. Push to ECR
6. Deploy to EKS
7. Post Deployment Health Check

---

## 🔐 Security

- Credentials stored in Jenkins Credentials Manager
- No hardcoded secrets
- IAM role attached to Jenkins EC2
- Artifact version tagging

---

## 📦 Sample Jenkinsfile Structure

pipeline {
  agent any

  stages {
    stage('Checkout') { steps { git 'repo-url' } }
    stage('Build') { steps { sh 'mvn clean install' } }
    stage('Docker Build') { steps { sh 'docker build -t app:latest .' } }
    stage('Push to ECR') { steps { sh 'docker push repo/app:latest' } }
    stage('Deploy') { steps { sh 'kubectl apply -f deployment.yaml' } }
  }
}

---

# 🔵 English Summary

Production pipeline ensures:

- Automated build and test
- Docker image versioning
- Secure credentials
- Zero manual deployment

---

# 📚 Official References

Jenkins Docs:
https://www.jenkins.io/doc/

AWS ECR:
https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html