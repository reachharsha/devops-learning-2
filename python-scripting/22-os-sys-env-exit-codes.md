---
title: "Python for DevOps Automation: 22 - OS, Sys, Env Vars, Exit Codes"
render_with_liquid: false
---

# Lesson 22 — OS, Sys, Env Vars, Exit Codes

DevOps automation lives inside an operating system.

You’ll constantly use:

- environment variables (config/secrets)
- exit codes (success/failure)
- current working directory
- PATH and filesystem paths

## Objectives

- Read environment variables safely
- Understand exit codes (0 vs non-zero)
- Use `os.getcwd()` and path joining
- Use `sys.exit()` / `raise SystemExit()`
- Avoid common beginner mistakes with env vars

## Mental Model

Your script is like a worker in a factory.

- The **OS** is the factory.
- **Environment variables** are labels stuck to the worker.
- **Exit code** is the worker’s final report number.

## Environment variables

Environment variables are key/value strings provided by the shell.

Example:

```bash
export APP_ENV=prod
```

Python reading:

```python
import os

env = os.getenv("APP_ENV")
print(env)
```

Important:

- `os.getenv()` returns `None` if missing
- env vars are always strings

## Exit codes

Exit code means:

- `0` success
- non-zero failure

In Python you can exit with:

```python
raise SystemExit(0)
raise SystemExit(1)
```

## Hands-on Lab — Fail with a clear message if env var missing

Create `require_env.py`:

```python
import os

token = os.getenv("API_TOKEN")
if not token:
    print("ERROR: API_TOKEN is required")
    raise SystemExit(1)

print("token length:", len(token))
```

Run without env var:

```bash
python3 require_env.py
```

Expected output:

```text
ERROR: API_TOKEN is required
```

Run with env var:

```bash
API_TOKEN=abc123 python3 require_env.py
```

Expected output:

```text
token length: 6
```

## Paths and current working directory

You can check where you are:

```python
import os
print(os.getcwd())
```

When building paths, prefer `pathlib` (Lesson 17). If using `os.path`:

```python
import os

path = os.path.join("logs", "app.log")
print(path)
```

## Common Mistakes (With Errors)

### Mistake 1 — Treating env var as int without converting

Bad:

```python
import os
timeout = os.getenv("TIMEOUT_SECONDS")
print(timeout + 1)
```

Typical error:

```text
TypeError: can only concatenate str (not "int") to str
```

Fix:

```python
timeout = int(os.getenv("TIMEOUT_SECONDS", "5"))
```

### Mistake 2 — Exiting but still printing success messages

Make sure your success print happens after validation.

## Quick Reference

- Env: `os.getenv("NAME")`
- Exit: `raise SystemExit(1)`
- CWD: `os.getcwd()`
- Join (old): `os.path.join(a, b)`
- Prefer: `pathlib.Path`

## Next

Next: [Lesson 23 — Running Commands (subprocess)](23-running-commands-subprocess.md)
