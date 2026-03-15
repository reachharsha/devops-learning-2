---
title: "Python Scripting: 34 - Concurrency (Intro)"
render_with_liquid: false
---

# Lesson 34 — Concurrency (Intro)

## Objectives

- Understand “concurrency” vs “parallelism”
- Learn when to use threads
- Run multiple I/O tasks faster (simple example)

## Concepts

For many network calls, threads can help because the script is waiting on I/O.

## Hands-on Lab

Create `threads_demo.py`:

```python
from concurrent.futures import ThreadPoolExecutor

import requests


def fetch(url):
    r = requests.get(url, timeout=10)
    return url, r.status_code


def main():
    urls = [
        "https://api.github.com",
        "https://example.com",
    ]

    with ThreadPoolExecutor(max_workers=5) as ex:
        for url, status in ex.map(fetch, urls):
            print(url, status)


if __name__ == "__main__":
    main()
```

## Quick Check

1) When do threads help in scripting?
2) What kind of tasks benefit most: CPU-heavy or I/O-heavy?

## Next

[Lesson 35: Mini Capstone](35-mini-capstone.md)
