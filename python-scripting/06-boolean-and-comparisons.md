---
title: "Python Scripting: 06 - Booleans & Comparisons"
render_with_liquid: false
---

# Lesson 06 — Booleans & Comparisons

## Objectives

- Understand `True` and `False`
- Use comparison operators
- Combine conditions using `and` / `or` / `not`

## Concepts

### Comparisons

- `==` equal
- `!=` not equal
- `< <= > >=` numeric comparisons

### Boolean operators

- `and` (both must be True)
- `or` (either can be True)
- `not` (flip)

## Hands-on Lab

Create `bool_demo.py`:

```python
age = 20

print(age >= 18)
print(age < 18)

is_weekend = True
has_work = False

print(is_weekend and has_work)
print(is_weekend or has_work)
print(not is_weekend)
```

## Quick Check

1) What is the difference between `=` and `==`?
2) When is `a and b` True?
3) When is `a or b` False?

## Next

[Lesson 07: Conditionals (if/elif/else)](07-conditionals.md)
