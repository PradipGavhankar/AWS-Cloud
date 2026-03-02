# ☁️ AWS Cloud Infrastructure & FinOps: The Production Blueprint

यह डॉक्युमेंट न केवल आपको इंटरव्यू में बेहतर दिखाएगा, बल्कि यह एक **Production-Grade Infrastructure** की समझ भी देता है। इसमें हमने AWS रिसोर्सेज को Terraform के जरिए बनाया है और साथ ही लागत (Cost) और सुरक्षा (Security) का पूरा ध्यान रखा है।

---

### 🧱 AWS Infrastructure as Code (Terraform)

```hcl
# 1. Provider & Version Constraint
# हिन्दी: हमेशा वर्जन लॉक करें ताकि कोड भविष्य में क्रैश न हो।
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

provider "aws" {
  region = "us-east-1"
}

# 2. VPC (VNet equivalent)
# हिन्दी: यह आपका नेटवर्क की बाउंड्री है।
resource "aws_vpc" "main" {
  cidr_block           = "10.0.0.0/16"
  enable_dns_hostnames = true
  tags = {
    Name        = "prod-vpc"
    Environment = "production"
    CostCenter  = "FinOps-Unit-01"
  }
}

# 3. Subnets (2 subnets in different AZs)
# हिन्दी: अलग-अलग ज़ोन में सबनेट बनाने से 'High Availability' बनी रहती है।
resource "aws_subnet" "subnet_1" {
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.1.0/24"
  availability_zone = "us-east-1a"
}

resource "aws_subnet" "subnet_2" {
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.2.0/24"
  availability_zone = "us-east-1b"
}

# 4. SSH Key Pair
# हिन्दी: आपके लोकल सिस्टम की 'Public Key' जिससे आप VM में सुरक्षित लॉगिन करेंगे।
resource "aws_key_pair" "deployer" {
  key_name   = "prod-key"
  public_key = "ssh-rsa AAAAB3Nza... user@laptop" # अपनी Key यहाँ डालें
}

# 5. Launch Template (VM Blueprint)
# हिन्दी: यह VM का ढांचा है। इसमें AMI, डिस्क साइज और टाइप तय होता है।
resource "aws_launch_template" "linux_tpl" {
  name_prefix   = "prod-linux-tpl"
  image_id      = "ami-0c7217cdde317cfec" # Amazon Linux 2023
  instance_type = "t3.micro"
  key_name      = aws_key_pair.deployer.key_name

  block_device_mappings {
    device_name = "/dev/xvda"
    ebs {
      volume_size = 20
      volume_type = "gp3" # Cost-effective & High Performance
    }
  }

  tag_specifications {
    resource_type = "instance"
    tags = { Name = "FinOps-VM" }
  }
}

# 6. Auto Scaling Group (VMSS Equivalent)
# हिन्दी: लोड बढ़ने पर 2 से 5 सर्वर तक अपने आप स्केल होगा।
resource "aws_autoscaling_group" "asg" {
  vpc_zone_identifier = [aws_subnet.subnet_1.id, aws_subnet.subnet_2.id]
  desired_capacity    = 2
  max_size            = 5
  min_size            = 2

  launch_template {
    id      = aws_launch_template.linux_tpl.id
    version = "$Latest"
  }
}

# ☁️ AWS Cloud Infrastructure: Monitoring & FinOps (Hindi Explained)

---

### 🧱 Full Terraform Code with Line-by-Line Hindi Comments

```hcl
# 1. Version Constraint
# हिन्दी: यहाँ हम बता रहे हैं कि हमें AWS का कम से कम 5.0 वर्जन चाहिए।
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0" # पुराने वर्जन से बचने के लिए इसे लॉक किया है।
    }
  }
}

# 2. SNS Topic (The Notification Hub)
# हिन्दी: यह एक 'अलर्ट स्टेशन' है, जो खबर (Alerts) फैलाने का काम करेगा।
resource "aws_sns_topic" "user_updates" {
  name = "billing-and-performance-alerts" # अलर्ट चैनल का नाम।
}

# SNS Subscription (Linking your Email)
# हिन्दी: यहाँ हम 'अलर्ट स्टेशन' को बता रहे हैं कि ईमेल पर मैसेज भेजो।
resource "aws_sns_topic_subscription" "email_target" {
  topic_arn = aws_sns_topic.user_updates.arn # ऊपर वाले SNS टॉपिक से जोड़ना।
  protocol  = "email"                        # सूचना भेजने का तरीका (Email)।
  endpoint  = "your-email@example.com"       # यहाँ आपका असली ईमेल आएगा।
}

# 3. CloudWatch Metric Alarm (The Guard Dog)
# हिन्दी: यह अलार्म 24x7 सर्वर की सेहत पर नज़र रखेगा।
resource "aws_cloudwatch_metric_alarm" "cpu_alarm" {
  alarm_name          = "High-CPU-Usage-Alarm" # अलार्म का एक यूनिक नाम।
  comparison_operator = "GreaterThanOrEqualToThreshold" # शर्त: क्या CPU 'Threshold' से ऊपर है?
  evaluation_periods  = "2"                    # लगातार 2 बार चेक करने पर ही अलार्म बजेगा।
  metric_name         = "CPUUtilization"       # हम 'CPU' की खपत नाप रहे हैं।
  namespace           = "AWS/EC2"              # यह सर्विस (EC2) का एड्रेस है।
  period              = "300"                  # हर 5 मिनट (300 सेकंड) में चेक करो।
  statistic           = "Average"              # 5 मिनट का 'औसत' (Average) निकालो।
  threshold           = "80"                   # सीमा: 80% से ऊपर जाते ही खतरा!
  alarm_description   = "This metric monitors ec2 cpu utilization" # छोटी जानकारी।
  alarm_actions       = [aws_sns_topic.user_updates.arn] # खतरा होने पर SNS को ट्रिगर करो।

  dimensions = {
    AutoScalingGroupName = aws_autoscaling_group.asg.name # किस सर्वर ग्रुप पर नज़र रखनी है।
  }
}

# 4. Auto Scaling Group (The Resource Manager)
# हिन्दी: यह ग्रुप लोड के हिसाब से सर्वर की संख्या बढ़ाएगा या घटाएगा।
resource "aws_autoscaling_group" "asg" {
  name                = "prod-asg" # ग्रुप का नाम।
  vpc_zone_identifier = ["subnet-12345", "subnet-67890"] # इन इलाकों (Subnets) में सर्वर रहेंगे।
  desired_capacity    = 2 # शुरुआत में हमेशा 2 सर्वर चालू रहेंगे।
  max_size            = 5 # ट्रैफिक बढ़ने पर अधिकतम 5 सर्वर तक जा सकते हैं।
  min_size            = 2 # कुछ भी हो जाए, 2 सर्वर हमेशा चालू रहेंगे।

  launch_template {
    id      = "lt-0123456789" # VM का ब्लूप्रिंट (AMI, Instance Type)।
    version = "$Latest"       # हमेशा सबसे लेटेस्ट वर्जन का इस्तेमाल करो।
  }
}
