---
title: "Python for DevOps Automation: 30 - Dataclasses & Type Hints"
render_with_liquid: false
---

# Lesson 30 — Dataclasses & Type Hints

As your scripts grow, you’ll pass around “records” like:

- host info
- check results
- config settings

`dataclasses` helps you represent structured data.
Type hints help you communicate expectations.

## Objectives

- Understand what type hints are (and what they are not)
- Create a simple `@dataclass`
- Convert dicts into dataclasses
- Avoid common beginner confusion

## Mental Model

Type hints are like **labels on boxes**.

- They don’t force the box to change.
- They help humans/tools understand what should be inside.

## Type hints (basic)

```python
def add(a: int, b: int) -> int:
    return a + b
```

Important:

- Python will still run even if you pass strings
- type hints are mainly for readability and tooling

## Dataclasses

Create `dataclass_demo.py`:

```python
from dataclasses import dataclass


@dataclass
class Host:
    name: str
    ip: str
    env: str


h = Host(name="web-01", ip="10.0.0.10", env="prod")
print(h)
print("name:", h.name)
```

Expected output:

```text
Host(name='web-01', ip='10.0.0.10', env='prod')
name: web-01
```

## Converting dict → dataclass

```python
data = {"name": "api-01", "ip": "10.0.1.10", "env": "stage"}
h = Host(**data)
```

## Common Mistakes (With Errors)

### Mistake 1 — Missing required field

```python
data = {"name": "api-01"}
Host(**data)
```

Typical error:

```text
TypeError: __init__() missing 2 required positional arguments: 'ip' and 'env'
```

Fix: validate input data before creating objects.

### Mistake 2 — Expecting type hints to enforce types

Type hints don’t stop this:

```python
add("1", "2")
```

Fix: validate critical inputs (config/env vars) at runtime.

## Quick Reference

- Type hints: `x: int`, `-> str`
- Dataclass: `@dataclass` + class with fields
- Dict to object: `Host(**d)`

## Next

Next: [Lesson 31 — Testing (unittest)](31-testing-unittest.md)
