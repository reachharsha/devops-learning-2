---
title: "AWS Fundamentals: 06 - Internet Gateway (IGW)"
render_with_liquid: false
---

# Lesson 06 — Internet Gateway (IGW)

## 1) What it is

An **Internet Gateway (IGW)** is the component that connects your VPC to the public internet.

## 2) Why it’s needed

If you want an internet-facing service (like a public load balancer), your VPC needs a way to send/receive internet traffic.

## 3) Where it fits

In AcmeShop:

- Public subnets route internet traffic to the IGW
- The ALB is placed in public subnets so users can reach it

## 4) How it works

Basic idea:

- You attach an IGW to a VPC
- Your public subnet route table includes `0.0.0.0/0 → IGW`

For true inbound access to an instance, other requirements also matter (we’ll cover security later):

- security group rules
- public IP / elastic IP (for direct instance access)

In our design, users do NOT reach EC2 directly; they reach the ALB.

## 5) Connections

- IGW is a route target
- Works with route tables and public IP addressing
- Still requires security group/NACL permissions

## 6) Real-world example

User opens `https://www.acmeshop.com`:

- DNS points to ALB
- ALB is in public subnets
- Public subnets have routes to IGW
- Traffic reaches the ALB through the IGW path

## 7) Common mistakes

- Attaching an IGW but forgetting the route table rule
- Thinking IGW alone makes things reachable (security groups still control)
- Exposing EC2 directly instead of using ALB

## 8) Interview explanation

"An Internet Gateway provides a path between a VPC and the internet. Public subnets are public because their route tables have a default route to the IGW. Inbound access still requires proper IP addressing and security group/NACL rules."

## Summary

- IGW = internet connectivity for public subnets
- Requires route table default route
- Not a security boundary

## Checkpoint questions

1) What two things are required for a public subnet to have internet routing?
2) Why don’t we expose EC2 directly in AcmeShop?
3) Does IGW provide security? Explain.

## Next

Next: [Lesson 07 — NAT Gateway (Private Subnet Outbound Internet)](07-nat-gateway.md)
