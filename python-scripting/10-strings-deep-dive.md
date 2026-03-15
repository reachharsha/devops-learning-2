---
title: "Python for DevOps Automation: 10 - Strings Deep Dive (DevOps)"
render_with_liquid: false
---

# Lesson 10 — Strings Deep Dive (DevOps)

## Objectives

- Use f-strings
- Use core string methods
- Parse simple DevOps text (URL → host)

## Concepts

Strings are immutable (you create new strings instead of editing in place).

## Hands-on Lab

Create `parse_url.py`:

```python
url = "https://api.example.com/v1/health"

if url.startswith("https://"):
    without_scheme = url[len("https://"):]
else:
    without_scheme = url

host = without_scheme.split("/")[0]

print(f"url={url}")
print(f"host={host}")
```

Expected output:

```text
url=https://api.example.com/v1/health
host=api.example.com
```

## Common mistakes

- IndexError from bad splitting

## DevOps use case

Logs, command output, URLs, configs all start as strings.

## Quick Reference

- f-string: `f"{name} {value:.2f}"`
- Methods: `strip split join replace startswith endswith`

## Next

[Lesson 11: Practice Pack (Part 1)](11-practice-pack-part1.md)
