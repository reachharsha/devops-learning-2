---
title: "AWS Fundamentals: 05 - Route Tables"
render_with_liquid: false
---

# Lesson 05 — Route Tables (How Traffic Knows Where to Go)

## 1) What it is

A **route table** is a set of rules that tells traffic where to go.

Think: "If the destination IP is X, send it to Y."

## 2) Why it’s needed

Without routing rules, subnets can’t:

- reach the internet
- reach other networks
- reach NAT gateways

Routing is what turns a subnet into “public” or “private”.

## 3) Where it fits

AcmeShop needs at least:

- a public route table (routes to IGW)
- a private route table (routes to NAT for outbound)

## 4) How it works

Route tables contain entries like:

- Destination: `10.0.0.0/16` → Target: `local` (inside VPC)
- Destination: `0.0.0.0/0` → Target: IGW or NAT

Important:

- `0.0.0.0/0` means “anywhere on the internet”

## 5) Connections

- Each subnet is associated with one route table
- IGW and NAT are route targets
- Security Groups/NACLs still control what’s allowed even if routing exists

## 6) Real-world example

Public subnets route:

- `0.0.0.0/0` → IGW

Private app subnets route:

- `0.0.0.0/0` → NAT Gateway

This lets app servers download updates without being reachable from the internet.

## 7) Common mistakes

- Adding `0.0.0.0/0` → IGW to a private subnet route table (accidentally makes it public)
- Forgetting to associate the route table with the subnet
- Thinking route tables provide security (they provide direction, not permission)

## 8) Interview explanation

"Route tables control network paths. I use a public route table with a default route to an internet gateway for public subnets, and private route tables with a default route to a NAT gateway for outbound internet from private subnets. Security is then enforced with security groups and NACLs."

## Summary

- Route tables = direction rules
- `0.0.0.0/0` is the default internet route
- Routing ≠ security

## Checkpoint questions

1) What does `0.0.0.0/0` mean?
2) What’s the difference between routing to IGW vs NAT?
3) Can route tables block traffic? Why/why not?

## Next

Next: [Lesson 06 — Internet Gateway (Inbound/Outbound Internet for Public Subnets)](06-internet-gateway.md)
