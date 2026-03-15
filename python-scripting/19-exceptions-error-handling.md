---
title: "Python for DevOps Automation: 19 - Exceptions & Error Handling"
render_with_liquid: false
---

# Lesson 19 — Exceptions & Error Handling

Errors happen in automation:

- missing files
- bad config
- permission issues
- network timeouts

Your goal is not “no errors”. Your goal is:

- **fail clearly** (good message)
- **fail safely** (non-zero exit code when needed)
- sometimes **recover** (retry or fallback)

## Objectives

- Use `try/except` to catch errors
- Understand exception types (`ValueError`, `KeyError`, `OSError`, etc.)
- Raise your own errors when something is not acceptable
- Use `finally` for cleanup

## Mental Model

Think of `try/except` like a **seatbelt**.

You still drive carefully, but if something goes wrong, you don’t want chaos.

## Basic pattern

```python
try:
    n = int("not-a-number")
except ValueError as e:
    print("bad input:", e)
```

Explain:

- `try:` block is “do the risky thing”
- `except ValueError:` catches only that kind of failure
- `as e` stores the error message object in variable `e`

## Multiple exception types

```python
try:
    # file may not exist
    text = open("missing.txt", "r").read()
except (OSError, IOError) as e:
    print("file error:", e)
```

## Raising your own error

If a config value is unacceptable, raise an exception.

```python
retries = 0

if retries < 1:
    raise ValueError("retries must be >= 1")
```

## Exiting with a non-zero code

For scripts, a common pattern is:

```python
raise SystemExit(1)
```

Exit code 0 means success. Non-zero means failure.

## Hands-on Lab — Safe config loader

Create `safe_load_config.py`:

```python
from pathlib import Path
import json


def load_config(path):
    try:
        text = Path(path).read_text(encoding="utf-8")
        cfg = json.loads(text)
    except OSError as e:
        print(f"CONFIG ERROR: cannot read '{path}': {e}")
        raise SystemExit(1)
    except json.JSONDecodeError as e:
        print(f"CONFIG ERROR: invalid JSON in '{path}': {e}")
        raise SystemExit(1)

    if not isinstance(cfg, dict):
        print("CONFIG ERROR: top-level JSON must be an object/dict")
        raise SystemExit(1)

    env = cfg.get("env")
    if env not in {"dev", "stage", "prod"}:
        print("CONFIG ERROR: env must be dev/stage/prod")
        raise SystemExit(1)

    return cfg


cfg = load_config("config.json")
print("OK:", cfg)
```

## `finally` for cleanup

`finally` runs whether you succeeded or failed.

```python
f = None

try:
    f = open("some.txt", "w")
    f.write("hello\n")
finally:
    if f is not None:
        f.close()
```

In modern Python, prefer `with open(...) as f:` (we’ll use that pattern soon).

## Common Mistakes

### Mistake 1 — Catching everything too early

Avoid:

```python
try:
    ...
except Exception:
    print("something failed")
```

This hides useful details. Catch specific exceptions when you can.

### Mistake 2 — Printing error but still exiting with success

If the script cannot continue, exit with non-zero:

```python
raise SystemExit(1)
```

## Quick Reference

- Catch: `try: ... except SomeError as e: ...`
- Multiple: `except (A, B) as e:`
- Raise: `raise ValueError("msg")`
- Script exit: `raise SystemExit(1)`
- Cleanup: `finally:`

## Next

Next: return to the course list: [Course Index](../index.html)
