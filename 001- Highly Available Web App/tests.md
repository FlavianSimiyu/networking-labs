# Scenario 01 – Tests

## Goal of Testing
The goal is to prove that the deployment is:
- reachable publicly through a single entry point (ALB)
- highly available across multiple instances
- self-healing when an instance fails
- able to scale when load increases (or at least show scaling policy behavior)
- observable through CloudWatch metrics and alarms

---

## Test 1: Public Access via Load Balancer
### Purpose
Confirm users can access the application through the ALB DNS name (not directly via EC2).

### Steps
1. Copy the ALB DNS name from the EC2 Load Balancers console.
2. Open it in a browser: `http://<ALB-DNS-NAME>`
3. Refresh multiple times.

### Expected Result
- The page loads successfully every time.
- (Optional if implemented) The page content changes between hosts (e.g., shows hostname), indicating distribution.

### Evidence to Capture
- Screenshot: browser showing the working page using ALB DNS.

---

## Test 2: Target Group Health Check Validation
### Purpose
Confirm the load balancer is routing traffic only to healthy instances.

### Steps
1. Open EC2 → Target Groups.
2. Select the target group attached to the ALB.
3. Go to the “Targets” tab.

### Expected Result
- Both instances are marked **Healthy**.

### Evidence to Capture
- Screenshot: target group showing 2 healthy targets.

---

## Test 3: Self-Healing (Instance Replacement by Auto Scaling)
### Purpose
Prove the system can recover from an instance failure without manual intervention.

### Steps
1. In EC2 → Auto Scaling Groups, identify the running instances.
2. Choose one instance and **terminate** it (simulate failure).
3. Monitor the Auto Scaling Group “Activity” tab.

### Expected Result
- ASG detects the capacity drop and launches a replacement instance automatically.
- Target group returns to the desired number of **healthy** targets.
- ALB URL remains reachable during the replacement.

### Evidence to Capture
- Screenshot: ASG activity history showing instance termination and new instance launch.
- Screenshot: target group returns to healthy targets after replacement.

---

## Test 4: Load Distribution (Optional but Recommended)
### Purpose
Show that traffic is being spread across instances.

### Steps
1. Refresh the ALB URL repeatedly.
2. If the web page displays hostname or instance ID, observe it changing.

### Expected Result
- Requests are served by different instances over time (if hostname display is enabled).

### Evidence to Capture
- Screenshot(s): showing different hostnames/instance identifiers.

---

## Test 5: Scaling Behavior (Scale-Out)
### Purpose
Prove that the environment can increase capacity under load (or at least that the policy triggers).

### Steps (Option A: if CPU-based scaling is configured)
1. Generate CPU load on one instance (method depends on OS/app).
2. Observe CloudWatch metrics and ASG desired capacity.

### Expected Result
- CloudWatch alarm transitions state (OK → ALARM).
- ASG increases desired capacity (e.g., from 2 to 3).

### Evidence to Capture
- Screenshot: CloudWatch alarm state change.
- Screenshot: ASG desired capacity increased and new instance launched.

### Notes
If scaling is not triggered due to time constraints, document:
- the configured scaling policy and thresholds
- current metrics showing readiness to scale

---

## Test 6: Monitoring & Alerting (CloudWatch)
### Purpose
Confirm that monitoring is in place and visible.

### Steps
1. Open CloudWatch metrics for EC2/ALB.
2. Confirm key metrics are visible (CPUUtilization, HealthyHostCount, RequestCount).
3. Verify alarms exist (even if not triggered).

### Expected Result
- Metrics appear and update.
- Alarm exists and is linked to the scaling action (or at minimum defined).

### Evidence to Capture
- Screenshot: CloudWatch metrics chart(s).
- Screenshot: CloudWatch alarm configured.

---

## Pass Criteria (Scenario Complete)
The scenario is considered complete if:
- ALB URL works reliably (Test 1)
- Target group shows healthy instances (Test 2)
- ASG replaces a terminated instance automatically (Test 3)
- CloudWatch monitoring is visible with at least one alarm configured (Test 6)

Scaling (Test 5) is strongly preferred but can be documented as configured if time-constrained.
