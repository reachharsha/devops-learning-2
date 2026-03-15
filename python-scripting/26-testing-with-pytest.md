---
title: "Python Scripting: 26 - Testing with pytest"
render_with_liquid: false
---

# Lesson 26 — Testing with pytest

## Objectives

- Understand what tests are and why they matter
- Write a simple unit test
- Run tests locally

## Concepts

Testing protects your automation from breaking when you change it.

`pytest` is a popular Python testing tool.

## Hands-on Lab

In a venv:

```bash
python -m pip install pytest
```

Create `calc.py`:

```python
def add(a, b):
    return a + b
```

Create `test_calc.py`:

```python
from calc import add


def test_add():
    assert add(2, 3) == 5
```

Run:

```bash
pytest -q
```

## Quick Check

1) What is a unit test?
2) Why do tests matter for automation?

## Next

[Lesson 27: Mocking & Fakes](27-mocking-and-fakes.md)
