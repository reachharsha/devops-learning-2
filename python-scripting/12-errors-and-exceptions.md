---
title: "Python Scripting: 12 - Errors & Exceptions"
render_with_liquid: false
---

# Lesson 12 — Errors & Exceptions

## Objectives

- Understand what exceptions are
- Catch exceptions with `try/except`
- Use `finally` for cleanup

## Concepts

### try/except

```python
try:
    risky()
except SomeError:
    handle()
```

### Don’t hide errors

Catching exceptions is useful, but you should still print/log something helpful.

## Hands-on Lab

Create `exceptions_demo.py`:

```python
def divide(a, b):
    return a / b

try:
    result = divide(10, 0)
    print(result)
except ZeroDivisionError as exc:
    print(f"Error: {exc}")
finally:
    print("Always runs")
```

## Quick Check

1) What is an exception?
2) When does `finally` run?

## Next

[Lesson 13: Paths with pathlib](13-pathlib-and-paths.md)
