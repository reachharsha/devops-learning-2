---
title: "AWS Fundamentals: 00 - START HERE"
render_with_liquid: false
---

# AWS Fundamentals (Absolute Beginner → End-to-End Architect)

You’re starting from zero AWS knowledge. Perfect.

By the end of this course you will be able to:

- Explain an end-to-end AWS application architecture
- Explain traffic flow: User → Route 53 → Load Balancer → App → Database → Response
- Place each AWS service correctly (networking, security, compute, storage, database, observability)
- Answer real-world and interview questions confidently

## The single architecture we’ll use for EVERYTHING

We will design one enterprise-style application and keep mapping every concept to it.

Application: **AcmeShop** (an e-commerce-style web application)

- Users browse the website and place orders
- The app serves web/API traffic
- Data is stored in a relational database
- Static assets (images) are stored in object storage
- Logs/metrics go to observability

High-level traffic flow (our always-on mental model):

User → DNS (Route 53) → Load Balancer → App (Compute) → Database (RDS) → Response

Infrastructure layout (our always-on mental model):

VPC → Subnets → Routing → Security → Compute → Storage → Database → Monitoring

## How to study (important)

This course teaches **one topic per lesson**.

At the end of every lesson you will get:

- a short summary
- 3–5 checkpoint questions

Rule: answer the questions (write your answers somewhere) before moving to the next lesson.

## What you need

- A computer with a browser
- (Optional) an AWS Free Tier account later

You do NOT need to create anything in AWS today to understand the concepts.

## Course map (00 → 20)

Foundations:

- 01: What AWS is, Regions/AZs, the “global vs regional” idea
- 02: Our reference architecture and traffic flow

Networking (foundation):

- 03: VPC + CIDR
- 04: Subnets (public vs private)
- 05: Route Tables
- 06: Internet Gateway (IGW)
- 07: NAT Gateway

Security:

- 08: IAM (users/roles/policies)
- 09: Security Groups
- 10: NACLs

Compute:

- 11: EC2
- 12: Auto Scaling
- 13: EKS (basic understanding)

Storage & Database:

- 14: S3
- 15: EBS
- 16: RDS

Traffic & Routing:

- 17: Load Balancers (ALB)
- 18: Route 53

Observability + Core principles:

- 19: CloudWatch basics
- 20: High Availability, Fault Tolerance, Scaling (tie it all together)

## Next

Next: [Lesson 01 — What Is AWS? (Regions, AZs, Global vs Regional)](01-what-is-aws-regions-az.md)
