---
title: "Python Scripting: 29 - dataclasses"
render_with_liquid: false
---

# Lesson 29 — dataclasses

## Objectives

- Model structured data cleanly
- Reduce boilerplate (`__init__`, `__repr__`)
- Use dataclasses for configuration and results

## Concepts

Dataclasses are great for automation because scripts often pass around structured data.

## Hands-on Lab

Create `dataclass_demo.py`:

```python
from dataclasses import dataclass


@dataclass
class Server:
    host: str
    port: int


s = Server(host="localhost", port=8080)
print(s)
```

## Quick Check

1) What problem do dataclasses solve?
2) Where would you use them in automation?

## Next

[Lesson 30: OOP (Basics)](30-oop-basics.md)
