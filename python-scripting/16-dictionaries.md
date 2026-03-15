---
title: "Python for DevOps Automation: 16 - Dictionaries (dict)"
render_with_liquid: false
---

# Lesson 16 — Dictionaries (`dict`)

A dictionary stores **key → value** pairs.

DevOps examples:

- config settings: `{"region": "us-east-1"}`
- metrics: `{"cpu": 91.2, "mem": 63.5}`
- parsed log fields: `{"service": "api", "level": "ERROR"}`

## Objectives

- Create dicts and access values by key
- Safely read missing keys with `.get()`
- Iterate keys/values
- Build dicts from simple `key=value` text
- Update dicts and remove keys safely
- Understand nested dicts (common in JSON)

## Mental Model (Analogy)

Think of a dict like a **labelled toolbox**.

- You don’t say “give me tool #3” (that’s a list).
- You say “give me the wrench” (that’s a dict: key = "wrench").

## Basics

```python
env = {
    "APP": "payments",
    "ENV": "prod",
    "REGION": "us-east-1",
}

print(env["APP"])     # direct lookup
print(env.get("TEAM"))  # safe lookup (returns None if missing)
```

### Why `.get()` matters

If a key is missing and you do `env["TEAM"]`, you get a `KeyError`.

## Hands-on Lab — Parse config-like text

Create `parse_config_text.py`:

```python
config_text = """\
APP=payments
ENV=prod
REGION=us-east-1
RETRIES=3
"""

config = {}

for line in config_text.splitlines():
    line = line.strip()
    if not line:
        continue
    if "=" not in line:
        continue
    key, value = line.split("=", 1)
    config[key] = value

print("APP:", config.get("APP"))
print("ENV:", config.get("ENV"))
print("MISSING:", config.get("MISSING", "<not set>"))
```

Expected output:

```text
APP: payments
ENV: prod
MISSING: <not set>
```

## Iterating dictionaries

```python
metrics = {"cpu": 91.2, "mem": 63.5}

for key, value in metrics.items():
    print(key, "=", value)
```

`items()` gives you `(key, value)` pairs.

Other useful views:

```python
print(metrics.keys())
print(metrics.values())
```

## Updating and removing keys

```python
cfg = {"env": "prod", "retries": 3}
cfg["retries"] = 5

removed = cfg.pop("retries")
print("removed:", removed)
print(cfg)
```

## Nested dictionaries (common in JSON)

API responses are often nested:

```python
resp = {
    "service": {"name": "api", "version": "1.2.3"},
    "status": {"healthy": True}
}

print(resp["service"]["name"])
print(resp.get("status", {}).get("healthy"))
```

## Common Mistakes (With Errors)

### Mistake 1 — KeyError

Bad:

```python
data = {"service": "api"}
print(data["level"])
```

Typical error:

```text
KeyError: 'level'
```

Fix: `data.get("level")` or check `if "level" in data:`.

### Mistake 2 — Overwriting a key by accident

If you set `config["ENV"] = "prod"` and later do `config["ENV"] = "dev"`, the old value is replaced.

That might be what you want — just be aware it happens.

### Mistake 3 — Treating a dict like a list

Bad:

```python
cfg = {"env": "prod"}
print(cfg[0])
```

Typical error:

```text
KeyError: 0
```

Because dict access is by key, not position.

## Quick Reference

- Create: `d = {"k": "v"}`
- Read: `d["k"]` (KeyError if missing)
- Safe read: `d.get("k")` or `d.get("k", default)`
- Add/update: `d["k"] = value`
- Iterate pairs: `for k, v in d.items():`
- Remove: `d.pop("k")`
- Nested safe get: `d.get("a", {}).get("b")`

## Next

Next: [Lesson 17 — Files & Paths (pathlib)](17-files-and-paths.md)
