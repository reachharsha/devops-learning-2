---
title: "AWS Fundamentals: 17 - Load Balancers (ALB)"
render_with_liquid: false
---

# Lesson 17 — Load Balancers (ALB)

## 1) What it is

An **Application Load Balancer (ALB)** distributes HTTP/HTTPS traffic across targets.

Targets can be:

- EC2 instances
- containers

## 2) Why it’s needed

You need:

- one stable entry point
- ability to scale multiple app servers
- health checks and failover

## 3) Where it fits

In AcmeShop:

- ALB is internet-facing in public subnets
- ALB forwards to app instances in private subnets

## 4) How it works

Flow:

1) User connects to ALB
2) ALB terminates TLS (HTTPS) or passes through
3) ALB checks which targets are healthy
4) ALB forwards request to a healthy target

ALB supports:

- path-based routing (e.g., `/api` vs `/static`)
- host-based routing

## 5) Connections

- Route 53 points DNS to ALB
- Security groups control inbound/outbound
- ASG registers instances into target group

## 6) Real-world example

AcmeShop has 6 app instances during a sale.

- ALB spreads traffic
- If one instance fails, ALB stops sending traffic to it

## 7) Common mistakes

- Putting ALB in only one subnet/AZ
- Allowing app instances to be public when they should be private
- Not enabling health checks correctly

## 8) Interview explanation

"I use an ALB as the public entry point for HTTP/HTTPS, deployed across multiple AZ subnets. It routes requests to targets in private subnets using health checks and integrates with Auto Scaling target groups for elasticity."

## Summary

- ALB is the front door
- Spreads load and improves availability

## Checkpoint questions

1) Why do we need an ALB if we have multiple EC2 instances?
2) Where should the ALB be placed (public/private)? Why?
3) What happens when a target becomes unhealthy?

## Next

Next: [Lesson 18 — Route 53 (DNS and Routing)](18-route53.md)
