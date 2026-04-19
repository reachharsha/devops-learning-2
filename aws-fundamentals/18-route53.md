---
title: "AWS Fundamentals: 18 - Route 53 (DNS)"
render_with_liquid: false
---

# Lesson 18 — Route 53 (DNS and Routing)

## 1) What it is

**Route 53** is AWS’s DNS service.

DNS maps names to targets.

Example:

- `www.acmeshop.com` → ALB DNS name

## 2) Why it’s needed

Humans use names.

Load balancers and servers have addresses that can change.

DNS gives you:

- stable entry name
- control over routing

## 3) Where it fits

It’s the first “AWS service” in the traffic path:

User → Route 53 → ALB → App → DB

## 4) How it works

Simplified:

1) User asks DNS for `www.acmeshop.com`
2) Route 53 returns a record that points to the ALB
3) Browser connects to the ALB

## 5) Connections

- ALB is the DNS target
- Certificates (not covered deeply here) secure HTTPS

## 6) Real-world example

Blue/green style migration:

- Move DNS from old ALB to new ALB
- Users gradually flow to the new environment

## 7) Common mistakes

- Confusing DNS with load balancing (DNS directs; ALB balances)
- Not understanding TTL (DNS caching)

## 8) Interview explanation

"Route 53 provides DNS. I use it to map the application domain to the ALB, so clients can reach a stable name while the underlying infrastructure scales and changes."

## Summary

- Route 53 = DNS
- First step in user traffic flow

## Checkpoint questions

1) What does DNS do in one sentence?
2) Why do we point DNS to ALB rather than directly to EC2?
3) What is TTL in DNS and why can it matter?

## Next

Next: [Lesson 19 — CloudWatch (Metrics, Logs, Alarms)](19-cloudwatch-basics.md)
