---
title: "Python for DevOps Automation: 09 - Operators & Type Conversion"
render_with_liquid: false
---

# Lesson 09 — Operators & Type Conversion

## Objectives

- Use arithmetic/comparison/logical operators
- Understand `is` vs `==`
- See conversion failures (ValueError)

## Concepts

- Arithmetic: `+ - * / // % **`
- Comparison: `== != < <= > >=`
- Logical: `and or not`

Use `is None` for None checks.

## Hands-on Lab

Create `retry_logic.py`:

```python
max_retries_text = input("Max retries: ")

try:
    max_retries = int(max_retries_text)
except ValueError as e:
    print("ValueError:", e)
    raise SystemExit(1)

attempt = 1
while attempt <= max_retries:
    print(f"Attempt {attempt}/{max_retries}")
    attempt += 1
```

## Common mistakes

- Using `=` inside `if` (SyntaxError)
- Using `== None` instead of `is None`

## DevOps use case

Thresholds and retries depend on operators.

## Quick Reference

- None check: `value is None`
- Convert: `int(x)` / `float(x)`

## Next

[Lesson 10: Strings Deep Dive (DevOps)](10-strings-deep-dive.md)
