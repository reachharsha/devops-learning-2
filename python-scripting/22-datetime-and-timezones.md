---
title: "Python Scripting: 22 - Dates/Times & Timezones"
render_with_liquid: false
---

# Lesson 22 — Dates/Times & Timezones

## Objectives

- Use `datetime` safely
- Understand naive vs timezone-aware datetimes
- Format timestamps for logs and filenames

## Concepts

### Common beginner pitfall

Timezones are tricky. For automation, prefer storing times in **UTC**.

## Hands-on Lab

Create `time_demo.py`:

```python
from datetime import datetime, timezone

now_utc = datetime.now(timezone.utc)
print("UTC:", now_utc.isoformat())

stamp = now_utc.strftime("%Y%m%d-%H%M%S")
print("stamp:", stamp)
```

## Quick Check

1) What is UTC?
2) Why is timezone-aware time safer in automation?

## Next

[Lesson 23: CLI Subcommands](23-cli-subcommands.md)
