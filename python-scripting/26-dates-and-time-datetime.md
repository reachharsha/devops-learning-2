---
title: "Python for DevOps Automation: 26 - Dates & Time (datetime)"
render_with_liquid: false
---

# Lesson 26 — Dates & Time (`datetime`)

DevOps automation often needs time:

- timestamps in logs
- calculating durations
- timeouts and scheduling

## Objectives

- Get the current time
- Understand naive vs timezone-aware datetimes
- Parse a simple timestamp
- Measure durations

## Mental Model

Time handling is like dealing with **time zones on a flight ticket**.

- If you don’t mention a timezone, people get confused.
- If you do mention it, things become consistent.

## Current time (timezone-aware)

```python
from datetime import datetime, timezone

now = datetime.now(timezone.utc)
print(now)
```

## Parsing ISO-like timestamps

Create `parse_time.py`:

```python
from datetime import datetime, timezone

text = "2026-03-15T10:05:30Z"

# Remove the trailing Z (Zulu = UTC) and parse
dt = datetime.strptime(text, "%Y-%m-%dT%H:%M:%SZ").replace(tzinfo=timezone.utc)

print("dt:", dt)
print("epoch:", int(dt.timestamp()))
```

Expected output (epoch value will differ if you change the date):

```text
dt: 2026-03-15 10:05:30+00:00
epoch: 1773578730
```

## Measuring durations

```python
from datetime import datetime
import time

start = datetime.now()
time.sleep(1)
end = datetime.now()

delta = end - start
print("seconds:", delta.total_seconds())
```

## Common Mistakes (With Errors)

### Mistake 1 — Mixing timezone-aware and naive

Typical error:

```text
TypeError: can't subtract offset-naive and offset-aware datetimes
```

Fix: use timezone-aware consistently (UTC is easiest).

## Quick Reference

- Now UTC: `datetime.now(timezone.utc)`
- Parse: `datetime.strptime(text, format)`
- Epoch: `dt.timestamp()`
- Duration: `end - start` → `timedelta.total_seconds()`

## Next

Next: [Lesson 27 — CSV (read/write)](27-csv-read-write.md)
