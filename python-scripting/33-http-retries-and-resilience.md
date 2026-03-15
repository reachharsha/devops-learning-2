---
title: "Python Scripting: 33 - HTTP Retries & Resilience"
render_with_liquid: false
---

# Lesson 33 — HTTP Retries & Resilience

## Objectives

- Understand transient failures
- Add timeouts (always)
- Implement simple retry logic

## Concepts

Networks fail. Your automation should handle temporary issues.

## Hands-on Lab

Create `retry_demo.py`:

```python
import time
import requests


def get_with_retry(url, retries=3, delay=1):
    last_exc = None
    for attempt in range(1, retries + 1):
        try:
            r = requests.get(url, timeout=5)
            r.raise_for_status()
            return r
        except Exception as exc:
            last_exc = exc
            time.sleep(delay)
    raise last_exc


if __name__ == "__main__":
    r = get_with_retry("https://api.github.com")
    print(r.status_code)
```

## Quick Check

1) What is a transient error?
2) Why always set a timeout?

## Next

[Lesson 34: Concurrency (Intro)](34-concurrency-intro.md)
