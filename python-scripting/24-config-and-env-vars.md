---
title: "Python Scripting: 24 - Config & Env Vars"
render_with_liquid: false
---

# Lesson 24 — Config & Env Vars

## Objectives

- Read environment variables (`os.environ`)
- Understand why config should be external
- Combine CLI args + env vars safely

## Concepts

Automation scripts often run in CI/CD. CI systems pass secrets and config via env vars.

## Hands-on Lab

Create `config_demo.py`:

```python
import os


def getenv(name, default=None):
    value = os.environ.get(name)
    return value if value is not None and value != "" else default


api_url = getenv("API_URL", "https://api.github.com")
timeout = int(getenv("TIMEOUT", "10"))

print("API_URL:", api_url)
print("TIMEOUT:", timeout)
```

Run:

```bash
python3 config_demo.py
API_URL=https://example.com TIMEOUT=3 python3 config_demo.py
```

## Quick Check

1) Why keep config outside code?
2) How do you read an env var in Python?

## Next

[Lesson 25: Secrets & Safety](25-secrets-and-safety.md)
