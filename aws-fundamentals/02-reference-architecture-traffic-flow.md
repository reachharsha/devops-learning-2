---
title: "AWS Fundamentals: 02 - Reference Architecture (Traffic Flow)"
render_with_liquid: false
---

# Lesson 02 — Reference Architecture (Traffic Flow)

This lesson locks in the one architecture we’ll keep referencing.

## 1) What it is (simple)

An AWS architecture is how you combine services to build a working application.

We’ll build **AcmeShop** with a common enterprise pattern:

- DNS
- Load balancing
- application compute
- database
- monitoring

## 2) Why it’s needed

Without an architecture, you end up with:

- random services glued together
- security gaps
- unclear traffic flow

Architecture = a plan you can explain and operate.

## 3) Where it fits

This is the blueprint. Every next lesson answers:

"Where does this service go in AcmeShop and why?"

## 4) How it works (basic flow)

### Our target traffic flow

1) User types `www.acmeshop.com` in the browser
2) **Route 53 (DNS)** resolves the name to the load balancer
3) **Load Balancer (ALB)** receives HTTPS traffic
4) ALB forwards to the **App** running on **EC2** (in private subnets)
5) App talks to **RDS** (database) to read/write orders
6) Response returns back through ALB to the user

### Our target network layout

Inside one region, across 2 AZs:

- One VPC
- Public subnets (for ALB, NAT gateway)
- Private subnets (for application servers)
- Private subnets for database

## 5) How it connects with other AWS services

This architecture will require:

- Networking: VPC, subnets, route tables, IGW, NAT
- Security: IAM, Security Groups, NACLs
- Compute: EC2 + Auto Scaling (and later EKS basics)
- Storage: S3 (static assets), EBS (EC2 disks)
- Database: RDS
- Observability: CloudWatch

## 6) Real-world example

Example request:

- User clicks “Place Order”
- App writes order to RDS
- App writes an order confirmation log to CloudWatch Logs
- User sees confirmation page

## 7) Common mistakes beginners make

- Putting EC2 (app servers) directly in public subnets just because it “works”
- Not being able to explain why NAT is needed
- Not separating app vs database network access

## 8) Interview explanation

"My baseline web architecture is Route 53 for DNS, an ALB in public subnets for inbound HTTPS, application instances in private subnets behind the ALB, and an RDS database in private subnets. Outbound internet access for patching goes through a NAT Gateway. Security is enforced with IAM for identities and Security Groups/NACLs for network boundaries, and CloudWatch for metrics/logs."

## Summary

- You now have one fixed mental model for traffic flow and layout
- Next lessons build the foundation network to make this possible

## Checkpoint questions

1) In one sentence, describe the traffic flow from user to database.
2) Which components should be in public subnets vs private subnets (and why)?
3) Why is the load balancer usually public but the app servers private?

## Next

Next: [Lesson 03 — VPC & CIDR (Your Private Network)](03-vpc-and-cidr.md)
