---
title: "Python Scripting: 25 - Secrets & Safety"
render_with_liquid: false
---

# Lesson 25 — Secrets & Safety

## Objectives

- Understand what “secrets” are (tokens, passwords, keys)
- Learn safe handling patterns
- Avoid logging sensitive data

## Concepts

### Never hard-code secrets

Bad:

```python
TOKEN = "abc123"  # don't do this
```

Better: read from environment variables.

### Don’t print secrets

If a CI log contains a token, it may leak.

## Hands-on Lab

Create `secrets_demo.py`:

```python
import os

token = os.environ.get("API_TOKEN")
if not token:
    raise SystemExit("Missing API_TOKEN")

print("Token loaded (not printing it). Length:", len(token))
```

Run:

```bash
API_TOKEN=example python3 secrets_demo.py
```

## Quick Check

1) Where should secrets live in CI?
2) Why is printing secrets dangerous?

## Next

[Lesson 26: Testing with pytest](26-testing-with-pytest.md)
