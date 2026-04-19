---
title: "AWS Fundamentals: 01 - What Is AWS? (Regions, AZs, Global vs Regional)"
render_with_liquid: false
---

# Lesson 01 — What Is AWS? (Regions, AZs, Global vs Regional)

## 1) What it is (simple)

AWS (Amazon Web Services) is a cloud platform that lets you rent:

- servers (compute)
- networks (virtual networking)
- storage (files/objects/disks)
- databases

Instead of buying hardware, you use AWS services.

## 2) Why it’s needed (problem it solves)

If you build on your laptop or one physical server, you hit problems:

- server can crash (downtime)
- you can’t handle sudden traffic spikes
- scaling takes time (buying hardware)
- security and access control are inconsistent

AWS gives you building blocks to design systems that are:

- scalable
- highly available
- secure

## AWS account basics (don’t skip this)

Before you create resources, you always work inside an **AWS Account**.

Beginner-safe guidance:

- The **root user** is the all-powerful account owner — don’t use it for day-to-day work
- Create an admin identity (AWS IAM Identity Center / SSO, or an IAM user in simple labs)
- Turn on MFA for important identities

You’ll also see different ways to access AWS:

- AWS Console (web UI)
- AWS CLI (command line)
- SDKs (Python/Java/etc.)

## Shared Responsibility Model (very important)

AWS security is shared:

- AWS is responsible for **security of the cloud** (data centers, hardware, foundational services)
- You are responsible for **security in the cloud** (your config, IAM permissions, network rules, encryption choices)

Example:

- AWS secures the physical building
- You must secure your S3 bucket permissions and your database password

## 3) Where it fits in our architecture

AWS is the entire “data center” for AcmeShop.

Everything we build (VPC, EC2, RDS, etc.) will live inside AWS.

## 4) How it works (basic internal flow)

### AWS Global Infrastructure

AWS is split into:

- **Regions**: geographic areas (example: `us-east-1`)
- **Availability Zones (AZs)**: isolated data centers inside a region (example: `us-east-1a`, `us-east-1b`)

Beginner rule:

- You deploy most resources **inside one region**
- For high availability, you spread across **multiple AZs**

### Global vs Regional vs AZ-scoped (critical mental model)

Some AWS services are:

- **Global** (conceptually one worldwide service)
- **Regional** (exists in a region)
- **AZ-scoped** (lives in one AZ)

You don’t need the full list yet, but keep this model.

Examples you will meet in this course:

- VPC: regional
- Subnet: AZ-scoped
- EC2: runs in a subnet (so it’s in an AZ)

## 5) How it connects with other AWS services

Regions/AZs affect everything:

- VPC is created in a region
- Subnets are created per AZ
- Load balancers can span multiple subnets (multiple AZs)
- Databases can be Multi-AZ for availability

## 6) Real-world example (MANDATORY)

AcmeShop availability:

- If we deploy only in one AZ and that AZ has an outage, AcmeShop is down.
- If we deploy across 2 AZs, the load balancer can send traffic to the healthy AZ.

## 7) Common mistakes beginners make

- Thinking “region = one data center” (it’s multiple AZs)
- Building everything in one AZ (single point of failure)
- Not understanding that some services are global vs regional
- Using the root user for everything
- Thinking AWS “automatically secures” your application (you still configure IAM/SG/NACL)

## 8) How to explain this in an interview

Use a clean explanation:

"AWS is organized into regions, and each region has multiple isolated availability zones. I design for high availability by spreading application components across at least two AZs within a region, so an AZ outage doesn’t take down the application."

## Summary

- Region = geographic area; AZ = isolated data center within a region
- Design for HA by using multiple AZs
- Keep global vs regional vs AZ-scoped in your head

## Checkpoint questions (answer before Lesson 02)

1) What is the difference between a Region and an AZ?
2) Why is deploying in 2 AZs safer than 1?
3) Name one resource that is regional and one that is AZ-scoped.

## Next

Next: [Lesson 02 — Our End-to-End Architecture (Traffic Flow)](02-reference-architecture-traffic-flow.md)
