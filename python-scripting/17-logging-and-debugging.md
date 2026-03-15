---
title: "Python Scripting: 17 - Logging & Debugging"
render_with_liquid: false
---

# Lesson 17 — Logging & Debugging

## Objectives

- Print vs logging
- Use `logging` levels: DEBUG/INFO/WARNING/ERROR
- Learn a simple debugging workflow

## Concepts

### Why logging?

For automation scripts, logs help you understand what happened later.

## Hands-on Lab

Create `logging_demo.py`:

```python
import logging

logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s %(levelname)s %(message)s",
)

logging.debug("This is debug")
logging.info("Starting")

try:
    value = int("not-a-number")
    logging.info("Value: %s", value)
except ValueError:
    logging.exception("Failed to parse integer")

logging.info("Done")
```

Run:

```bash
python3 logging_demo.py
```

## Quick Check

1) Why is `logging` better than only `print()` for scripts?
2) What does `logging.exception()` include?

## Next

[Lesson 18: Build a CLI with argparse](18-cli-argparse.md)
