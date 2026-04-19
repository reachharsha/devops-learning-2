---
title: "AWS Fundamentals: 16 - RDS (Relational Database)"
render_with_liquid: false
---

# Lesson 16 — RDS (Relational Database Service)

## 1) What it is

**RDS** is a managed relational database service.

You can run database engines like:

- MySQL
- PostgreSQL

AWS manages many operational tasks for you.

## 2) Why it’s needed

Your application needs a durable place to store structured data:

- users
- orders
- inventory

Databases require:

- backups
- patching
- monitoring
- high availability

RDS reduces your operational burden.

## 3) Where it fits

In AcmeShop:

- RDS stores orders and user data
- RDS is deployed in **private db subnets**
- Only app servers can reach it (SG rules)

## 4) How it works

Key concepts:

- DB instance lives in your VPC
- Subnet group defines which subnets it can use
- Security group controls who can connect

High availability option:

- **Multi-AZ** deployment (standby in another AZ)

## 5) Connections

- VPC/Subnets: placement
- Security Groups: allow app → db on port 5432/3306
- CloudWatch: metrics
- IAM: controls who can manage RDS resources (not the DB login)

## 6) Real-world example

AcmeShop order write:

- App receives request
- App validates input
- App writes order to RDS
- App returns success

If one AZ fails and RDS is Multi-AZ, AWS can fail over.

## 7) Common mistakes

- Putting RDS in a public subnet
- Allowing `0.0.0.0/0` inbound on DB port
- Forgetting backups/retention settings

## 8) Interview explanation

"RDS is a managed relational database in my VPC. I place it in private subnets, restrict inbound access to only the application security group, enable Multi-AZ for availability, and monitor it with CloudWatch and backups."

## Summary

- RDS stores structured data
- Keep it private and tightly controlled
- Use Multi-AZ for HA

## Checkpoint questions

1) Why must RDS usually be in private subnets?
2) What does Multi-AZ give you?
3) What SG rule should exist between app and DB?

## Next

Next: [Lesson 17 — Load Balancers (ALB)](17-load-balancers-alb.md)
