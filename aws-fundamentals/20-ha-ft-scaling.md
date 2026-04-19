---
title: "AWS Fundamentals: 20 - High Availability, Fault Tolerance, Scaling"
render_with_liquid: false
---

# Lesson 20 — High Availability, Fault Tolerance, Scaling (Tie It All Together)

This is the capstone: you will describe the full architecture end-to-end.

## 1) What these are (simple)

- **High Availability (HA)**: the system stays up during common failures
- **Fault Tolerance (FT)**: the system continues operating even when components fail
- **Scaling**: handle more traffic by adding resources (scale out) or making them bigger (scale up)

## 2) Why they’re needed

Real systems face:

- instance failures
- AZ outages
- traffic spikes
- software bugs

You design so the business continues.

## 3) Where they fit in AcmeShop

Walk the architecture and map HA/FT/scaling:

- Route 53: stable DNS entry point
- ALB across 2 AZs: survives an AZ issue
- ASG across 2 AZs: replaces bad instances, scales out
- App in private subnets: reduces attack surface
- RDS Multi-AZ: improves database availability
- NAT per AZ (optional): improves outbound resiliency
- CloudWatch: detects issues and triggers alarms/scaling

## 4) How traffic flows (end-to-end)

Say this clearly:

1) User queries DNS: Route 53 returns the ALB
2) User connects to ALB over HTTPS
3) ALB selects a healthy app instance (EC2) in a private subnet
4) App reads/writes to RDS
5) App returns response → ALB → user

## 5) Security at each layer

- IAM: who can manage AWS and what the app can access
- Security Groups:
  - internet → ALB (443)
  - ALB → app (8080)
  - app → DB (5432/3306)
- NACLs: optional subnet guardrails
- Private subnets: reduce direct exposure

## 6) Real-world example

Scenario: one EC2 instance crashes during a sale.

- ALB health checks mark it unhealthy
- ALB stops routing to it
- ASG launches a replacement
- CloudWatch shows the spike and scaling event

User impact: minimal.

## 7) Common mistakes

- Saying “Multi-AZ” but only deploying app servers in one AZ
- Treating stateful data like it lives on EC2 disks
- No clear security boundaries between tiers
- No monitoring/alarms

## 8) Interview explanation (strong answer template)

"For an internet-facing application, I use Route 53 for DNS and an ALB in public subnets across two AZs. The application runs on EC2 in an Auto Scaling Group in private subnets, and only the ALB security group can reach the app tier. The database runs in RDS in private subnets with Multi-AZ enabled and access restricted to the app security group. Outbound internet access for patching uses NAT gateways. I use CloudWatch for metrics/logs and alarms for error rates and scaling triggers. This design supports high availability, self-healing, and scaling while keeping the attack surface minimal."

## Summary

- HA/FT/scaling are achieved by designing across AZs, using managed services, and automating healing
- You can now narrate the full system end-to-end

## Checkpoint questions (final)

1) Explain the full traffic flow in 5 steps.
2) Name 3 design choices that improve availability.
3) Name 3 security controls in this architecture.
4) What would you monitor in CloudWatch first?
5) If the database becomes a bottleneck, what are your next steps (high-level)?

## Next

Next: return to the course list: [Course Index](../index.html)
