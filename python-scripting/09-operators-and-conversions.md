---
title: "Python for DevOps Automation: 09 - Operators & Type Conversion"
render_with_liquid: false
---

# Lesson 09 — Operators & Type Conversion

## Objectives

By the end, you can:

- Explain what an operator is
- Use arithmetic, comparison, and logical operators
- Understand precedence (what runs first)
- Use `is None` correctly
- Handle conversion failures (`ValueError`)

## What is an operator?

An operator is a symbol/keyword that tells Python to do something with values.

Examples:

- `+` adds numbers
- `>` compares values
- `and` combines conditions

## Arithmetic operators

- `+ - *` add/subtract/multiply
- `/` division (returns float)
- `//` floor division (drops the decimal)
- `%` remainder (modulo)
- `**` power

Examples:

```python
print(5 / 2)   # 2.5
print(5 // 2)  # 2
print(5 % 2)   # 1
```

## Comparison operators

- `==` equals, `!=` not equals
- `< <= > >=` numeric comparisons

```python
disk = 87
print(disk >= 80)  # True
```

## Logical operators

- `and` both sides True
- `or` at least one True
- `not` flip boolean

## Precedence (order of operations)

```python
print(3 + 4 * 2)    # 11
print((3 + 4) * 2)  # 14
```

When unsure, add parentheses.

## `==` vs `is` and `None`

- `==` compares values
- `is` checks identity (same object)

For `None`, use:

```python
if value is None:
    ...
```

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

### Mistake 1 — Using `=` inside `if`

Bad:

```python
if max_retries = 3:
    print("oops")
```

Typical error:

```text
SyntaxError: cannot assign to name here
```

### Mistake 2 — Forgetting precedence

Use parentheses if you need a specific order.

### Mistake 3 — Comparing to None

Prefer `is None` over `== None`.

## DevOps use case

Thresholds and retries depend on operators.

## Quick Reference

- None check: `value is None`
- Convert: `int(x)` / `float(x)`
- Precedence: use parentheses

## Next

[Lesson 10: Strings Deep Dive (DevOps)](10-strings-deep-dive.md)
