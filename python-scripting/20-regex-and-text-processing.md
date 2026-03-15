---
title: "Python Scripting: 20 - Regex & Text Processing"
render_with_liquid: false
---

# Lesson 20 — Regex & Text Processing

## Objectives

- Understand what regex is used for
- Extract patterns from text
- Avoid common regex mistakes

## Concepts

Regex (regular expressions) is a way to match patterns in text.

Python uses the `re` module.

## Hands-on Lab

Create `regex_demo.py`:

```python
import re

text = "User alice@example.com logged in from 10.20.30.40"

email = re.search(r"[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}", text)
ip = re.search(r"\b(?:\d{1,3}\.){3}\d{1,3}\b", text)

print("email:", email.group(0) if email else None)
print("ip:", ip.group(0) if ip else None)
```

Run:

```bash
python3 regex_demo.py
```

## Quick Check

1) What module provides regex support?
2) What does `re.search()` return when it finds nothing?

## Next

Next batch will continue with APIs, testing, typing, and packaging.
