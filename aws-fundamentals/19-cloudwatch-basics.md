---
title: "AWS Fundamentals: 19 - CloudWatch Basics"
render_with_liquid: false
---

# Lesson 19 — CloudWatch (Metrics, Logs, Alarms)

## 1) What it is

**CloudWatch** is AWS’s core observability service.

It includes:

- Metrics (numbers over time)
- Logs (text events)
- Alarms (notify/trigger actions)

## 2) Why it’s needed

If you can’t see what your system is doing, you can’t operate it.

CloudWatch helps you answer:

- Is the app healthy?
- Is CPU high?
- Are there errors?
- Did latency spike?

## 3) Where it fits

Across the entire AcmeShop architecture:

- ALB metrics (requests, errors)
- EC2 metrics (CPU, network)
- RDS metrics (connections, latency)

## 4) How it works

Metrics:

- AWS services publish metrics automatically

Logs:

- Your app/OS can send logs (agent or service integration)

Alarms:

- Trigger when metric crosses a threshold
- Can notify or scale (ASG)

## 5) Connections

- Auto Scaling uses CloudWatch alarms for scaling
- Operations uses alarms for alerting

## 6) Real-world example

AcmeShop alert:

- Alarm: ALB 5xx errors > threshold
- Alarm: EC2 CPU > 80% triggers scale-out

## 7) Common mistakes

- Only monitoring CPU and missing app-level errors
- No alarms (metrics exist but nobody is notified)
- Not keeping logs long enough for troubleshooting

## 8) Interview explanation

"CloudWatch provides metrics, logs, and alarms. I monitor ALB, EC2, and RDS metrics, centralize logs, and create alarms for error rates and latency. I also integrate scaling policies with CloudWatch alarms for automated elasticity."

## Summary

- CloudWatch = visibility + alerting
- Ties into scaling and operations

## Checkpoint questions

1) What’s the difference between a metric and a log?
2) Give one example of a useful alarm for AcmeShop.
3) How can CloudWatch connect to Auto Scaling?

## Next

Next: [Lesson 20 — High Availability, Fault Tolerance, Scaling (Tie It All Together)](20-ha-ft-scaling.md)
