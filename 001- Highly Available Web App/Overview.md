# Architectural Overview

## 1. Understanding the Problem

The task requires designing a public-facing web application that remains available despite:
- Sudden increases in user traffic
- Failure of individual compute instances

From an architectural perspective, this immediately rules out:
- Single EC2 instance deployments
- Manual scaling
- Direct public access to individual servers

The solution must therefore support **high availability, scalability, and fault tolerance**.

---

## 2. Key Requirements Identified

From the scenario, the following technical requirements are implied:

- **High Availability:**  
  The application must continue serving traffic even if one instance fails.

- **Load Distribution:**  
  Incoming user traffic should be spread across multiple instances.

- **Automatic Scaling:**  
  The number of running instances should adjust based on demand without manual intervention.

- **Monitoring & Visibility:**  
  The system must expose health and performance metrics and raise alerts when thresholds are breached.

- **Secure Access to AWS Services:**  
  EC2 instances should interact with AWS services using IAM roles, not hardcoded credentials.

---

## 3. Selected AWS Services and Rationale

### Amazon EC2
Provides the compute layer where the web application runs.

### Application Load Balancer (ALB)
- Distributes incoming HTTP traffic across multiple EC2 instances.
- Performs health checks and routes traffic only to healthy targets.
- Acts as the single public entry point to the application.

### Auto Scaling Group (ASG)
- Ensures a minimum number of EC2 instances are always running.
- Automatically replaces unhealthy or terminated instances.
- Scales the number of instances up or down based on demand.

### IAM Role for EC2
- Grants EC2 instances permission to interact with AWS services securely.
- Eliminates the need to store AWS credentials on the instance.

### Amazon CloudWatch
- Collects metrics such as CPU utilization.
- Enables alarms that can trigger scaling actions or notify operators.

---

## 4. High-Level Traffic Flow

1. A user accesses the application using the ALB’s public DNS name.
2. The ALB receives the request and evaluates target health.
3. Traffic is forwarded to a healthy EC2 instance in the Auto Scaling Group.
4. CloudWatch continuously monitors instance metrics.
5. If thresholds are exceeded, the Auto Scaling Group adjusts capacity automatically.

---

## 5. Design Assumptions and Scope

- The application is stateless and does not require persistent local storage.
- The deployment spans multiple Availability Zones for resilience.
- Cost efficiency is prioritized by using free-tier eligible instance types and deleting resources after testing.
- Advanced features such as HTTPS termination and CI/CD pipelines are intentionally out of scope for this scenario.

---

## 6. Why This Architecture Is Appropriate

This architecture reflects a common real-world pattern used to host:
- Public websites
- Simple web applications
- Front-end tiers of larger systems

It balances simplicity, reliability, and scalability while remaining cost-conscious and suitable for a small engineering team.
