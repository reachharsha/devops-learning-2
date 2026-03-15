---
title: "Python Scripting: 03 - Variables & Types"
render_with_liquid: false
---

# Lesson 03 — Variables & Types

## Objectives

- Store data in variables
- Learn common types: `str`, `int`, `float`, `bool`
- Use `type()` to inspect values

## Concepts

### Variables

A variable is a name that points to a value.

```python
name = "Harsha"
age = 25
```

### Types

Examples:

- `"hello"` is a `str` (string)
- `10` is an `int`
- `3.14` is a `float`
- `True` is a `bool`

## Hands-on Lab

Create `types_demo.py`:

```python
name = "Alice"
age = 30
height = 1.75
is_student = False

print(name, type(name))
print(age, type(age))
print(height, type(height))
print(is_student, type(is_student))
```

Run:

```bash
python3 types_demo.py
```

## Quick Check

1) What does `type(value)` return?
2) Is `"10"` an integer?
3) Can a variable change to a different type later in Python?

## Next

[Lesson 04: Strings & Printing](04-strings-and-printing.md)
