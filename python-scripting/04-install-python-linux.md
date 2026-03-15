---
title: "Python for DevOps Automation: 04 - Install Python on Linux"
render_with_liquid: false
---

# Lesson 04 — Install Python on Linux

## Objectives

- Install Python 3 on Ubuntu/Debian
- Install Python 3 on CentOS/RHEL
- Understand `python` vs `python3`
- Verify install

## Concepts

### Verify first

```bash
python3 --version
```

## Hands-on Lab

### Ubuntu/Debian

```bash
sudo apt update
sudo apt install -y python3 python3-pip python3-venv
python3 --version
python3 -m pip --version
```

### CentOS/RHEL

```bash
sudo dnf install -y python3 python3-pip
python3 --version
```

If `dnf` isn’t available, use `yum`.

## Common mistakes

- Running `python` and getting an unexpected version

Fix: use `python3`.

## DevOps use case

Your scripts run on servers. Installing/verifying Python quickly is essential.

## Quick Reference

- Verify: `python3 --version`
- Ubuntu: `apt install python3 python3-pip python3-venv`
- RHEL-like: `dnf install python3 python3-pip`

## Next

[Lesson 05: pip, venv, requirements.txt](05-pip-venv-requirements.md)
