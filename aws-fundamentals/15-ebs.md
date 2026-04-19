---
title: "AWS Fundamentals: 15 - EBS (Elastic Block Store)"
render_with_liquid: false
---

# Lesson 15 — EBS (Elastic Block Store)

## 1) What it is

**EBS** is a virtual hard disk for EC2.

- block storage
- attached to an EC2 instance

## 2) Why it’s needed

EC2 needs disks for:

- OS volume
- application files
- temporary storage

EBS provides persistent storage beyond instance memory.

## 3) Where it fits

In AcmeShop:

- Each EC2 instance has an EBS root volume
- The app might store temporary files (but important data should go to RDS/S3)

## 4) How it works

- EBS volumes are created in a specific AZ
- Volume attaches to an EC2 instance in the same AZ

Important: EBS is not multi-AZ by itself.

## 5) Connections

- EC2 uses EBS volumes
- Snapshots can back up EBS (stored in S3 under the hood)

## 6) Real-world example

If an EC2 instance is replaced by Auto Scaling, its local disk contents may not be preserved.

So you keep state in:

- RDS (database)
- S3 (objects)

and treat EC2 + EBS as replaceable.

## 7) Common mistakes

- Storing important state only on EBS for an Auto Scaling app
- Forgetting EBS is AZ-scoped

## 8) Interview explanation

"EBS provides block storage volumes for EC2. Volumes are AZ-scoped, so for highly available apps I avoid storing critical state on instance disks and instead use managed services like RDS and S3."

## Summary

- EBS = disks for EC2
- AZ-scoped; treat app servers as disposable when using ASG

## Checkpoint questions

1) Why is EBS considered AZ-scoped?
2) Why is storing critical data on EC2/EBS risky in Auto Scaling?
3) Where should AcmeShop store critical data instead?

## Next

Next: [Lesson 16 — RDS (Managed Relational Database)](16-rds.md)
