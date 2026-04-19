---
title: "AWS Fundamentals: 13 - EKS Basics"
render_with_liquid: false
---

# Lesson 13 — EKS (Kubernetes on AWS) Basics

This course is not a full Kubernetes course, but you must understand where EKS fits.

## 1) What it is

**EKS (Elastic Kubernetes Service)** is AWS’s managed Kubernetes control plane.

Kubernetes is a system for running containerized applications.

## 2) Why it’s needed

Organizations use Kubernetes to:

- standardize deployments
- run many microservices
- scale and roll out updates safely

EKS reduces operational burden by managing the Kubernetes control plane.

## 3) Where it fits in our architecture

AcmeShop can run either:

- on EC2 instances (simple)
- or as containers in EKS (more advanced)

Traffic flow stays similar:

User → Route 53 → ALB → (EC2 app OR EKS services) → RDS

## 4) How it works (basic flow)

High-level:

- EKS manages the Kubernetes API/control plane
- Worker nodes run your pods (can be EC2-based)
- Ingress/load balancing routes traffic into the cluster

## 5) How it connects

- IAM: roles for cluster, nodes, and pod permissions
- VPC/Subnets: EKS runs inside your VPC
- Load Balancer: often ALB via Ingress
- CloudWatch: metrics/logs

## 6) Real-world example

AcmeShop microservices:

- `catalog-service`, `orders-service`, `payments-service`
- Each service runs as pods in EKS
- ALB routes `/orders` to `orders-service`

## 7) Common mistakes

- Using EKS too early without understanding networking/IAM basics
- Thinking EKS removes all responsibility (you still manage workloads, security, upgrades planning)

## 8) Interview explanation

"EKS is managed Kubernetes. I use it when we need container orchestration and standardized deployments. Networking and security still rely on VPC design, security groups, and IAM roles. Traffic commonly enters through an ALB/Ingress and reaches services/pods, which then connect to data services like RDS."

## Summary

- EKS = managed Kubernetes control plane
- It sits in the same network/security world (VPC/IAM)

## Checkpoint questions

1) What problem does Kubernetes/EKS solve compared to raw EC2?
2) Does EKS remove the need for VPC and IAM knowledge? Why?
3) In our traffic flow, where does EKS sit?

## Next

Next: [Lesson 14 — S3 (Object Storage)](14-s3.md)
