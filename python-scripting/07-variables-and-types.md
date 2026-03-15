---
title: "Python for DevOps Automation: 07 - Variables & Data Types"
render_with_liquid: false
---

# Lesson 07 — Variables & Data Types

## Objectives

- Understand variables (labeled box idea)
- Learn core types: str/int/float/bool/None
- Learn `type()` and `id()`
- Learn mutability

## Real-world analogy

Variable = labeled box:

```text
hostname  ->  "web-01"
```

`=` means “assign”, not “math equals”.

## Concepts

### Types

- `str` text
- `int` whole numbers
- `float` decimal
- `bool` True/False
- `None` missing value

### Mutability

- Mutable: list/dict/set
- Immutable: str/int/float/tuple

## Hands-on Lab

Create `types_devops.py`:

```python
hostname = "web-01"
retry_count = 3
cpu_load = 0.75
service_up = True
last_error = None

print("hostname:", hostname, type(hostname))
print("retry_count:", retry_count, type(retry_count))
print("cpu_load:", cpu_load, type(cpu_load))
print("service_up:", service_up, type(service_up))
print("last_error:", last_error, type(last_error))

print("id(hostname):", id(hostname))
```

## Common mistakes

- Using reserved keywords as variable names (SyntaxError)

## DevOps use case

Variables hold config values, parsed log fields, and API response data.

## Quick Reference

- Assign: `name = value`
- Types: `str int float bool None`
- Check: `type(x)`
- Mutable: list/dict/set

## Next

[Lesson 08: Output, Input, Comments](08-output-input-comments.md)
