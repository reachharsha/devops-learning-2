---
title: "Python for DevOps Automation: 28 - HTTP APIs (requests)"
render_with_liquid: false
---

# Lesson 28 — HTTP APIs (`requests`)

Modern DevOps automation often calls APIs:

- cloud APIs
- internal service health endpoints
- CI/CD systems

The most common Python library is `requests`.

## Objectives

- Understand HTTP basics (GET, status codes)
- Make a request with timeout
- Parse JSON responses
- Handle errors safely

## Mental Model

HTTP is like sending a form to a receptionist:

- you ask (request)
- you get an answer (response)
- the response has a status code (200 OK, 404 Not Found, 500 Error)

## Install `requests`

In your venv:

```bash
python3 -m pip install requests
```

## GET request + JSON parsing

Create `get_json.py`:

```python
import requests

url = "https://httpbin.org/json"  # public test endpoint

try:
    r = requests.get(url, timeout=5)
    r.raise_for_status()
except requests.RequestException as e:
    print("HTTP ERROR:", e)
    raise SystemExit(1)

data = r.json()
print("keys:", sorted(list(data.keys())))
```

Expected output (keys may vary depending on endpoint version):

```text
keys: ['slideshow']
```

## Common Mistakes (With Errors)

### Mistake 1 — No timeout

If you don’t set a timeout, a request can hang forever.

Fix: always pass `timeout=...`.

### Mistake 2 — Not checking status codes

If the server returns 500, `r.json()` may fail.

Fix: call `r.raise_for_status()`.

### Mistake 3 — Offline or DNS issues

You might see errors like:

```text
requests.exceptions.ConnectionError: ...
```

Fix: check network/DNS, or test with a local endpoint.

## Quick Reference

- Install: `pip install requests`
- GET: `requests.get(url, timeout=5)`
- Status check: `r.raise_for_status()`
- JSON: `r.json()`
- Errors: `requests.RequestException`

## Next

Next: [Lesson 29 — Advanced File Patterns (glob, safe writes)](29-advanced-files-glob-safe-writes.md)
