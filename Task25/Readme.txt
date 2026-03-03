TASK 1 — Multi-Region Highly Available Web Application (AWS)

Objective: Deploy a fault-tolerant web application across multiple Availability Zones using AWS services: VPC, ALB, Auto Scaling, EC2, S3, and CloudWatch.

Architecture Diagram (ASCII):
                  Internet
                      |
                      v
      +-------------------------------+
      |  Application Load Balancer    |
      |        (Public Subnets)       |
      +-------------------------------+
             |                 |
             v                 v
   +----------------+   +----------------+
   | EC2 Instance   |   | EC2 Instance   |
   | Private Subnet |   | Private Subnet |
   |      AZ1       |   |      AZ2       |
   +----------------+   +----------------+
             |                 |
             v                 v
   +----------------+   +----------------+
   | NAT Gateway    |   | NAT Gateway    |
   | Public Subnet  |   | Public Subnet  |
   +----------------+   +----------------+
             |                 |
             v                 v
                  Internet

   +-------------------------------+
   |        Amazon S3 Bucket       |
   |  (Static Assets for EC2)      |
   +-------------------------------+

   [CloudWatch Alarm: CPU > 70%] --> Auto Scaling Group --> EC2 Instances.

Step-by-Step Deployment (Short Version):

1. VPC Setup:

Create VPC: 10.0.0.0/16
Create 2 Public Subnets (10.0.1.0/24, 10.0.2.0/24)
Create 2 Private Subnets (10.0.3.0/24, 10.0.4.0/24)
Attach Internet Gateway

Public Route Table → 0.0.0.0/0 → IGW

2. NAT Gateway:

Launch NAT in Public Subnet
Private Route Table → 0.0.0.0/0 → NAT

3. EC2 Instances:

Launch 2 EC2 in Private Subnets
Security Group: HTTP (80) → ALB SG ,SSH (22) → Your IP

4. S3 Website & User Data:
Create S3 Bucket (my-static-assetts-pragya) with website files
Create IAM Role: EC2-S3-Read-Role → Attach AmazonS3ReadOnlyAccess
Attach role to Launch Template

Use this User Data script:

#!/bin/bash
yum update -y
yum install -y httpd aws-cli
systemctl start httpd
systemctl enable httpd
rm -rf /var/www/html/*
aws s3 sync s3://my-static-assetts-pragya /var/www/html
chown -R apache:apache /var/www/html
chmod -R 755 /var/www/html
systemctl restart httpd

5. Application Load Balancer:

Type: Application, Internet-facing
Public Subnets AZ1 & AZ2
Security Group: HTTP 80 → 0.0.0.0/0
Create Target Group → Register EC2 instances

6. Auto Scaling Group:

Launch Template: Use above EC2/User Data
Min: 2, Desired: 2, Max: 4
Subnets: Private Subnet 1 & 2
Attach Target Group

7. CloudWatch Alarm:

Metric: EC2 CPU > 70% → Trigger Auto Scaling

8. Testing:

Access ALB DNS in browser → Verify web app loads