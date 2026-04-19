---
title: "AWS Fundamentals: 07 - NAT Gateway"
render_with_liquid: false
---

# Lesson 07 — NAT Gateway (Private Subnet Outbound Internet)

## 1) What it is

A **NAT Gateway** lets resources in **private subnets** access the internet **outbound**, without allowing inbound internet connections to them.

NAT = Network Address Translation.

## 2) Why it’s needed

Private app servers still need to:

- download OS updates
- pull packages
- call external APIs

But we do NOT want the internet to initiate connections to those servers.

NAT provides outbound-only access.

## 3) Where it fits

In AcmeShop:

- NAT Gateway lives in a public subnet
- Private subnets route `0.0.0.0/0` to NAT

## 4) How it works (basic flow)

1) App server in private subnet sends traffic to an internet destination
2) Route table sends that traffic to NAT Gateway
3) NAT Gateway uses a public IP to talk to the internet
4) Response returns to NAT, then back to the app server

Important:

- NAT is for **outbound** from private subnets
- Inbound from internet to private subnet is still blocked by design

## 5) Connections

- Requires IGW (because NAT is in a public subnet)
- Requires correct route table association
- Works with Security Groups/NACLs (they must allow outbound)

## 6) Real-world example

AcmeShop app servers (private subnets) need to download security updates.

- They use NAT Gateway to reach package repositories
- No one on the internet can connect to the app servers directly

## 7) Common mistakes

- Putting NAT Gateway in a private subnet (it must be reachable to the internet)
- Forgetting to assign the private subnet route `0.0.0.0/0 → NAT`
- Using one NAT for multiple AZs without understanding AZ failure/cost tradeoffs

## 8) Interview explanation

"A NAT Gateway enables outbound internet access for instances in private subnets. Private route tables point the default route to NAT, while public subnets route to an IGW. This supports patching and external API calls without exposing private instances to inbound internet traffic."

## Summary

- NAT = outbound internet for private subnets
- NAT sits in a public subnet; private subnets route to it

## Checkpoint questions

1) Why does NAT Gateway belong in a public subnet?
2) What route table change makes a private subnet able to reach the internet?
3) What security benefit does NAT provide?

## Next

Next: [Lesson 08 — IAM (Users, Roles, Policies)](08-iam-users-roles-policies.md)
