---
title: "Python Scripting: 21 - HTTP & APIs (requests)"
render_with_liquid: false
---

# Lesson 21 — HTTP & APIs (requests)

## Objectives

- Understand HTTP at a high level (GET/POST)
- Call an API from Python
- Parse JSON responses

## Concepts

### What is an API?

An API is a service you can talk to over the network. Most modern APIs use HTTP and JSON.

### Install `requests`

`requests` is not part of the standard library.

In a venv:

```bash
python -m pip install requests
```

## Hands-on Lab

Create `api_demo.py`:

```python
import requests

url = "https://api.github.com"
response = requests.get(url, timeout=10)

print("status:", response.status_code)
data = response.json()
print("keys:", sorted(list(data.keys()))[:10])
```

Run:

```bash
python3 api_demo.py
```

## Quick Check

1) What is the difference between GET and POST?
2) How do you convert a JSON response to Python data?

## Next

[Lesson 22: Dates/Times & Timezones](22-datetime-and-timezones.md)
