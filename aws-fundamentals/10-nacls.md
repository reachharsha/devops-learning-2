---
title: "AWS Fundamentals: 10 - NACLs (Network ACLs)"
render_with_liquid: false
---

# Lesson 10 — NACLs (Subnet-Level Guardrails)

## 1) What it is

A **Network ACL (NACL)** is a firewall at the **subnet** level.

It controls:

- inbound rules
- outbound rules

## 2) Why it’s needed

Security Groups are usually enough.

NACLs are useful as extra guardrails, especially in enterprises, for example:

- block known bad IP ranges at the subnet boundary
- enforce a stricter “deny by default” posture

## 3) Where it fits

NACLs apply to subnets in AcmeShop:

- public subnet NACL
- private app subnet NACL
- private db subnet NACL

Often you keep NACLs simple and rely on SGs for fine-grained rules.

## 4) How it works

Important NACL behavior:

- NACLs are **stateless**
  - you must allow inbound and outbound explicitly

Rules are evaluated in order (lowest rule number first).

## 5) Connections

- Subnet has one NACL association
- NACL + SG together determine if traffic can pass

Beginner guidance:

- Use SGs for most application rules
- Use NACLs for broad subnet boundary policies

## 6) Real-world example

If the security team wants to block a bad IP range from reaching public subnets:

- Add a NACL deny rule for that CIDR on inbound

Your ALB SG might still allow 443, but the NACL blocks it earlier.

## 7) Common mistakes

- Forgetting ephemeral ports (return traffic)
- Denying something with NACL and then wondering why SG changes don’t help
- Overcomplicating NACLs early as a beginner

## 8) Interview explanation

"Security Groups are stateful and attached to resources, while NACLs are stateless and applied at the subnet level. I typically rely on security groups for tier-to-tier access control and use NACLs for coarse-grained subnet guardrails like blocking ranges or enforcing baseline policy."

## Summary

- NACL = subnet-level firewall
- Stateless (must allow both directions)
- Good for guardrails; SGs handle most app security

## Checkpoint questions

1) What is the key difference between SG and NACL (stateful vs stateless)?
2) Why can NACLs break traffic even if SG rules look correct?
3) Where would you apply NACLs in AcmeShop?

## Next

Next: [Lesson 11 — EC2 (Compute)](11-ec2.md)
