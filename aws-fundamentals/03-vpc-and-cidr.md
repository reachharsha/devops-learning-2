---
title: "AWS Fundamentals: 03 - VPC & CIDR"
render_with_liquid: false
---

# Lesson 03 — VPC & CIDR (Your Private Network)

## 1) What it is (simple)

**VPC (Virtual Private Cloud)** is your private network in AWS.

Inside a VPC you place:

- subnets
- EC2 instances
- load balancers
- databases

**CIDR** is the IP address range for that VPC (example: `10.0.0.0/16`).

## 2) Why it’s needed

You need a network boundary so you can control:

- who can talk to whom
- routing to internet vs private
- segmentation (app vs database)

Without a VPC, you can’t build secure, isolated architectures.

## 3) Where it fits in our architecture

AcmeShop lives inside **one VPC**.

Everything else (subnets, route tables, security groups) attaches to this VPC.

## 4) How it works (basic internal flow)

### CIDR basics

CIDR is like reserving a block of addresses.

Example:

- `10.0.0.0/16` means:
  - network range from `10.0.0.0` to `10.0.255.255`
  - you can create many smaller subnets inside

Beginner-friendly rule:

- Use a private range like `10.0.0.0/16`
- Split it into smaller `/24` subnets per AZ

## 5) How it connects with other AWS services

- Subnets must be created inside a VPC
- Security Groups are attached to ENIs inside a VPC
- NAT/IGW attach to the VPC
- RDS must be placed in subnets within a VPC

## 6) Real-world example

AcmeShop VPC:

- VPC CIDR: `10.0.0.0/16`
- Public subnets:
  - `10.0.0.0/24` (AZ-a)
  - `10.0.1.0/24` (AZ-b)
- Private app subnets:
  - `10.0.10.0/24` (AZ-a)
  - `10.0.11.0/24` (AZ-b)
- Private db subnets:
  - `10.0.20.0/24` (AZ-a)
  - `10.0.21.0/24` (AZ-b)

## 7) Common mistakes beginners make

- Picking a CIDR that overlaps with their office/home network (causes VPN problems later)
- Making the VPC too small (no room for growth)
- Not planning subnets per AZ

## 8) Interview explanation

"A VPC is an isolated network boundary in AWS. I choose a private CIDR like 10.0.0.0/16, then create public and private subnets across multiple AZs. This gives me segmentation and control over routing and security for the application."

## Summary

- VPC = your private network boundary
- CIDR = IP range you allocate
- Plan CIDR/subnets early to avoid redesign

## Checkpoint questions

1) What problem does a VPC solve?
2) What does `10.0.0.0/16` mean in simple terms?
3) Why might overlapping CIDRs be a problem later?

## Next

Next: [Lesson 04 — Subnets (Public vs Private)](04-subnets-public-private.md)
