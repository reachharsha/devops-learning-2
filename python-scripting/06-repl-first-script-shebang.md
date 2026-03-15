---
title: "Python for DevOps Automation: 06 - REPL, First Script, Shebang"
render_with_liquid: false
---

# Lesson 06 — REPL, First Script, Shebang

## Objectives

- Use the REPL
- Run a `.py` script
- Use shebang
- Make scripts executable

## Concepts

### REPL

Start:

```bash
python3
```

Exit:

```python
exit()
```

### Shebang

```text
#!/usr/bin/env python3
```

## Hands-on Lab

Create `healthcheck.py`:

```python
#!/usr/bin/env python3

print("OK: script started")
```

Run:

```bash
python3 healthcheck.py
chmod +x healthcheck.py
./healthcheck.py
```

Expected output:

```text
OK: script started
```

## Common mistakes

- Forgetting execute permission → `Permission denied`

Fix: `chmod +x file.py`.

## DevOps use case

Executable scripts are easy to run from cron and CI.

## Quick Reference

- REPL: `python3`
- Run: `python3 file.py`
- Executable: `chmod +x file.py` then `./file.py`

## Next

[Lesson 07: Variables & Data Types](07-variables-and-types.md)
