# Scenario 01 – Verification Evidence

## Purpose
This document lists the proof artifacts (screenshots and outputs) that demonstrate the scenario requirements were met.

---

## A. Architecture & Configuration Evidence

### 1) Load Balancer
- [ ] Screenshot: ALB overview page showing:
  - Scheme: internet-facing
  - Listener: HTTP :80
  - VPC and subnets
  - Security group attached

### 2) Target Group
- [ ] Screenshot: Target group “Targets” tab showing **Healthy** targets (expected: 2)
- [ ] Screenshot: Target group health check configuration (path/port)

### 3) Auto Scaling Group
- [ ] Screenshot: ASG details showing:
  - Desired capacity (2)
  - Min (2), Max (4)
  - Launch template attached
  - Subnets/AZs used

### 4) EC2 Instances (created by ASG)
- [ ] Screenshot: EC2 instances list filtered by ASG tag/name showing 2 running instances
- [ ] Screenshot: one instance “Details” showing:
  - Instance type (micro)
  - AZ placement
  - Security group

### 5) IAM Role (Good Practice)
- [ ] Screenshot: IAM role attached to EC2 instances (instance profile)
- [ ] Screenshot: role permissions summary (high level)

---

## B. Functional Proof (End-to-End)

### 6) Public Access through ALB
- [ ] Screenshot: browser showing the web page loaded via `http://<ALB-DNS-NAME>`

### 7) High Availability Proof (Self-Healing)
- [ ] Screenshot: ASG “Activity” showing:
  - instance terminated
  - replacement instance launched
- [ ] Screenshot: Target group returning to **Healthy** targets after replacement

---

## C. Monitoring & Alerting Proof (CloudWatch)

### 8) Metrics Visibility
- [ ] Screenshot: CloudWatch metric for **EC2 CPUUtilization**
- [ ] Screenshot: CloudWatch metric for **ALB HealthyHostCount** (or TargetGroup metric)
- [ ] Screenshot: CloudWatch metric for **ALB RequestCount** (optional but good)

### 9) Alarm Configuration
- [ ] Screenshot: CloudWatch alarm configured (threshold + action)
- [ ] Screenshot: Alarm state change (OK → ALARM) if triggered during testing

---

## D. Optional CLI Proof (Nice-to-have)
If using AWS CLI, capture outputs (paste them below) for extra credibility.

### 10) Describe Load Balancer
```bash
aws elbv2 describe-load-balancers --names <ALB_NAME>

### 11) Describe Target Health
aws elbv2 describe-target-health --target-group-arn <TARGET_GROUP_ARN>

### 12) Describe Auto Scaling Group
aws autoscaling describe-auto-scaling-groups --auto-scaling-group-names <ASG_NAME>

### 13) Describe Instances by Tag
aws ec2 describe-instances --filters "Name=tag:aws:autoscaling:groupName,Values=<ASG_NAME>"