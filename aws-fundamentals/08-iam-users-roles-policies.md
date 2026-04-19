---
title: "AWS Fundamentals: 08 - IAM (Users, Roles, Policies)"
render_with_liquid: false
---

# Lesson 08 — IAM (Users, Roles, Policies)

Networking controls traffic paths. IAM controls **who can do what** in AWS.

## 1) What it is

**IAM (Identity and Access Management)** is AWS’s permission system.

Key pieces:

- **User**: a human identity
- **Role**: an identity assumed by a service (or a user temporarily)
- **Policy**: a document that defines permissions

## 2) Why it’s needed

Without IAM, anyone with access could:

- delete servers
- read secrets
- open security holes

IAM gives least-privilege access control.

## 3) Where it fits in our architecture

AcmeShop uses IAM in multiple places:

- Humans (admins/devs) use IAM users/SSO to access AWS
- EC2 instances use an IAM **role** to access S3 or CloudWatch
- (Later) EKS uses roles for nodes/pods

## 4) How it works (basic internal flow)

Policy is evaluated when you call an AWS API.

Example:

- EC2 app wants to read an image from S3
- App calls S3 API
- IAM checks if the EC2 role has permission

Beginner rule:

- Permissions are **deny by default**
- You explicitly allow actions

## 5) How it connects

- EC2 instance profile attaches a role to an instance
- S3 bucket policies can complement IAM policies
- CloudWatch agent can use IAM role permissions

## 6) Real-world example

We want app servers to upload logs/reports to S3.

- Create IAM role: `AcmeShopAppRole`
- Attach policy allowing `s3:PutObject` to `acmeshop-reports/*`
- Attach role to EC2 instances

Now the app can write to S3 without hardcoding AWS keys.

## 7) Common mistakes

- Creating access keys and putting them in code (avoid)
- Giving `AdministratorAccess` to everything
- Confusing roles vs users

## 8) Interview explanation

"IAM controls permissions in AWS using policies. I avoid long-term access keys in applications by using IAM roles attached to compute (like EC2) so the app can access S3/CloudWatch with least privilege. For humans, I prefer SSO and role-based access with minimal permissions."

## Summary

- User = human; Role = assumed identity; Policy = permissions
- Prefer roles for applications (no embedded keys)
- Use least privilege

## Checkpoint questions

1) What’s the difference between an IAM user and an IAM role?
2) Why are access keys in code a bad idea?
3) In AcmeShop, what would you use IAM for on EC2?

## Next

Next: [Lesson 09 — Security Groups (Instance-Level Firewall)](09-security-groups.md)
