---
title: "Python for DevOps Automation: 24 - Logging (logging module)"
render_with_liquid: false
---

# Lesson 24 — Logging (Instead of `print`)

In automation, `print()` is okay for learning, but logging is better:

- levels: DEBUG/INFO/WARNING/ERROR
- consistent formatting
- optionally write to a file

## Objectives

- Understand log levels
- Configure basic logging
- Log exceptions with context
- Avoid common logging mistakes

## Mental Model

`print()` is like shouting.

`logging` is like using a **radio with channels** (levels).

## Basic logging

Create `logging_demo.py`:

```python
import logging

logging.basicConfig(
    level=logging.INFO,
    format="%(levelname)s %(name)s %(message)s",
)

log = logging.getLogger("healthcheck")

log.debug("debug message")
log.info("starting")
log.warning("slow response")
log.error("failed")
```

Expected output (DEBUG is hidden because level=INFO):

```text
INFO healthcheck starting
WARNING healthcheck slow response
ERROR healthcheck failed
```

## Logging exceptions

```python
import logging

logging.basicConfig(level=logging.INFO)
log = logging.getLogger("demo")

try:
    int("abc")
except ValueError:
    log.exception("could not convert value")
```

`log.exception(...)` prints a traceback automatically.

## Common Mistakes (With Errors)

### Mistake 1 — Logging configured too late

If you call `basicConfig()` after some logging already happened, it may not apply.

Fix: configure logging near the top of your script.

### Mistake 2 — Using f-strings for expensive debug logs

If debug is off, you still build the string.

Better pattern (lets logging handle formatting):

```python
log.debug("value=%s", value)
```

## Quick Reference

- Setup: `logging.basicConfig(level=logging.INFO, format=...)`
- Logger: `log = logging.getLogger("name")`
- Levels: `debug info warning error`
- Exception: `log.exception("msg")`

## Next

Next: [Lesson 25 — Regular Expressions (re)](25-regular-expressions.md)
