---
title: "Python Scripting: 27 - Mocking & Fakes"
render_with_liquid: false
---

# Lesson 27 — Mocking & Fakes

## Objectives

- Understand why mocking is used
- Mock network calls in tests
- Avoid flaky tests

## Concepts

Automation often calls APIs. Tests should not depend on real networks.

Python’s standard library has `unittest.mock`.

## Hands-on Lab

Create `fetcher.py`:

```python
import requests


def fetch_status(url):
    r = requests.get(url, timeout=10)
    return r.status_code
```

Create `test_fetcher.py`:

```python
from unittest.mock import Mock, patch

import fetcher


def test_fetch_status():
    fake_response = Mock(status_code=200)
    with patch("requests.get", return_value=fake_response):
        assert fetcher.fetch_status("https://example.com") == 200
```

## Quick Check

1) Why mock API calls in tests?
2) What makes tests “flaky”?

## Next

[Lesson 28: Type Hints (Basics)](28-type-hints-basics.md)
