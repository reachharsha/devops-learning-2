---
title: "Python for DevOps Automation: 08 - Output, Input, Comments"
render_with_liquid: false
---

# Lesson 08 — Output, Input, Comments

## Objectives

- Learn `print()` (sep/end)
- Learn `input()` (string)
- Convert input safely

## Concepts

`input()` always returns a string.

## Hands-on Lab

Create `disk_threshold.py`:

```python
value_text = input("Enter disk usage percent (0-100): ")

try:
    value = int(value_text)
except ValueError:
    print("ERROR: enter a number like 80")
    raise SystemExit(1)

if value >= 80:
    print("ALERT: disk usage high")
else:
    print("OK: disk usage normal")
```

## Common mistakes

- Doing math with strings → `TypeError`

Fix: `int(text)` or `float(text)`.

## DevOps use case

All automation needs input validation.

## Quick Reference

- Print: `print(a, b, sep="-", end="\n")`
- Input: `text = input("...")`
- Convert: `int(text)` / `float(text)`

## Next

[Lesson 09: Operators & Type Conversion](09-operators-and-conversions.md)
