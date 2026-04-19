---
title: "AWS Fundamentals: 12 - Auto Scaling"
render_with_liquid: false
---

# Lesson 12 — Auto Scaling (Scale and Heal Automatically)

## 1) What it is

**Auto Scaling** automatically adds/removes EC2 instances based on demand or health.

Core concept: **Auto Scaling Group (ASG)**.

## 2) Why it’s needed

If you have only 1 server:

- it becomes overloaded under traffic
- if it crashes, your app is down

Auto Scaling solves:

- scaling out under load
- replacing unhealthy instances

## 3) Where it fits

In AcmeShop:

- App servers run in an ASG across 2 AZs
- ALB sends traffic to the ASG instances

## 4) How it works

An ASG has:

- desired capacity (how many instances you want)
- min and max
- health checks
- a launch template (how to create a new instance)

Flow:

1) Load increases
2) Scaling policy triggers (example: CPU > 60%)
3) ASG launches new EC2 instances
4) Instances register with target group
5) ALB starts sending traffic to them

## 5) How it connects

- EC2: instances created by ASG
- ALB target group: where instances register
- CloudWatch alarms: often used to trigger scaling

## 6) Real-world example

AcmeShop seasonal sale:

- Baseline: 2 instances
- During sale: scale to 10 instances
- After sale: scale back down

## 7) Common mistakes

- Setting max too low (can’t scale)
- Not spreading across AZs
- Confusing “scale up” (bigger instance) with “scale out” (more instances)

## 8) Interview explanation

"I run the application tier in an Auto Scaling Group across multiple AZs. ASG maintains desired capacity, replaces unhealthy instances, and scales out based on CloudWatch metrics. Traffic is routed via an ALB target group."

## Summary

- ASG provides self-healing + scaling
- Works tightly with ALB and CloudWatch

## Checkpoint questions

1) What does an ASG do when an instance becomes unhealthy?
2) What’s the difference between scale out and scale up?
3) Why do we use min/max/desired capacity?

## Next

Next: [Lesson 13 — EKS (Kubernetes on AWS) Basics](13-eks-basics.md)
