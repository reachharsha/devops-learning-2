---
title: "AWS Fundamentals: 09 - Security Groups"
render_with_liquid: false
---

# Lesson 09 — Security Groups (Instance-Level Firewall)

## 1) What it is

A **Security Group (SG)** is a virtual firewall for AWS resources like:

- EC2 instances
- Load Balancers
- RDS databases

SGs control:

- inbound rules (who can connect in)
- outbound rules (where it can connect out)

## 2) Why it’s needed

Even if your resources are in private subnets, you still need rules for:

- ALB → App
- App → DB

SGs are the main layer of network security in AWS.

## 3) Where it fits

AcmeShop SG design (simple and powerful):

- `alb-sg`: allows inbound 443 from the internet; outbound to app
- `app-sg`: allows inbound from `alb-sg` only; outbound to db
- `db-sg`: allows inbound from `app-sg` only

## 4) How it works

Important SG behavior:

- SGs are **stateful**
  - if inbound is allowed, return traffic is automatically allowed

Also:

- SG rules can reference another SG (very common)

## 5) Connections

- Route tables decide where traffic could go
- SG decides whether that traffic is allowed
- NACLs (next lesson) add another subnet-level layer

## 6) Real-world example

ALB receives user HTTPS traffic.

- `alb-sg` inbound: allow TCP 443 from `0.0.0.0/0`
- ALB forwards to EC2 on port 80/8080
- `app-sg` inbound: allow TCP 8080 from `alb-sg`

Now:

- users can’t connect to app servers directly
- only ALB can

## 7) Common mistakes

- Opening app SG inbound to `0.0.0.0/0` "just to test" and forgetting to close it
- Confusing SGs with NACLs
- Not restricting DB access to app-only

## 8) Interview explanation

"Security Groups are stateful virtual firewalls attached to resources. I design layered SGs: internet to ALB only, ALB to app only, app to DB only. I prefer referencing SGs rather than IPs, which keeps rules stable as instances scale."

## Summary

- SGs control inbound/outbound at resource level
- Stateful, and can reference other SGs
- Core to tiered security

## Checkpoint questions

1) What does “stateful” mean for a security group?
2) Why is “SG referencing SG” useful in Auto Scaling?
3) In AcmeShop, which SG should allow inbound from the internet?

## Next

Next: [Lesson 10 — NACLs (Subnet-Level Guardrails)](10-nacls.md)
