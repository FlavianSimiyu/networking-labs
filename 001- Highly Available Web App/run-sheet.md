## Build (once)
- [ ] Create ALB + listener :80
- [ ] Create Target Group + health checks
- [ ] Create Launch Template (user-data installs web page)
- [ ] Create Auto Scaling Group (min 2 desired 2 max 4) across 2 subnets
- [ ] Confirm 2 instances launched

## Test + Capture Evidence (in this exact order)
### 1) Public access
- [ ] Open ALB DNS in browser (screenshot → verification A6)

### 2) Target health
- [ ] Target group shows 2 healthy targets (screenshot → verification A2)

### 3) Self-healing
- [ ] Terminate 1 instance
- [ ] ASG launches replacement (screenshot → verification B7)
- [ ] Target group returns to healthy (screenshot → verification B7)

### 4) Monitoring
- [ ] Open CloudWatch CPU metric (screenshot → verification C8)
- [ ] Create/confirm alarm exists (screenshot → verification C9)

## Cleanup
- [ ] Delete ASG
- [ ] Delete Launch Template (or versions)
- [ ] Delete ALB
- [ ] Delete Target Group
- [ ] Delete unused security groups (only if created new ones)
