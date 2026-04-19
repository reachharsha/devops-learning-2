---
title: "AWS Fundamentals: 04 - Subnets (Public vs Private)"
render_with_liquid: false
---

# Lesson 04 — Subnets (Public vs Private)

## 1) What it is

A **subnet** is a smaller network inside your VPC.

Key rule:

- A subnet lives in **one AZ**.

## 2) Why it’s needed

Subnets let you separate components:

- things that must receive internet traffic (public)
- things that must never be directly reachable (private)

This separation is the foundation of secure architecture.

## 3) Where it fits

AcmeShop uses 3 subnet “layers” across 2 AZs:

- Public subnets: load balancer + NAT gateway
- Private app subnets: EC2 application servers
- Private db subnets: RDS

## 4) How it works

### What makes a subnet “public”?

A subnet is considered **public** if its route table has a route to an **Internet Gateway (IGW)**.

### What makes a subnet “private”?

A subnet is **private** if it does NOT route directly to the IGW.

Private subnets can still reach the internet *outbound* using a NAT Gateway (we’ll cover this).

## 5) How it connects

- Subnets connect to route tables
- EC2 instances are launched into subnets
- ALB spans multiple public subnets
- RDS uses a subnet group (multiple subnets)

## 6) Real-world example

AcmeShop placement:

- ALB in public subnets (needs inbound from users)
- EC2 in private app subnets (only inbound from ALB)
- RDS in private db subnets (only inbound from app)

## 7) Common mistakes

- Thinking “public subnet” automatically means “secure enough”
- Putting databases in public subnets
- Using only one AZ (single point of failure)

## 8) Interview explanation

"I design with public and private subnets across at least two AZs. Public subnets host internet-facing components like an ALB and NAT. Application and database tiers live in private subnets, reachable only from allowed sources via security groups."

## Summary

- Subnet = AZ-scoped slice of your VPC
- Public vs private is defined by routing (IGW route)
- Use subnet layers for security and clarity

## Checkpoint questions

1) What makes a subnet public?
2) Why do we put app servers in private subnets?
3) Can a private subnet access the internet? If yes, how?

## Next

Next: [Lesson 05 — Route Tables (How Traffic Knows Where to Go)](05-route-tables.md)
