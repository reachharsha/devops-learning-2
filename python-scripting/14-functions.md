---
title: "Python for DevOps Automation: 14 - Functions (def, return)"
render_with_liquid: false
---

# Lesson 14 — Functions (def, return)

Functions help you **package logic** into reusable building blocks.

In automation, this is how you avoid copying the same code into 10 scripts.

## Objectives

- Define a function with `def`
- Pass inputs via parameters
- Return values using `return`
- Know the difference between “printing” and “returning”

## Mental Model (Analogy)

A function is like a **runbook step** that you can call whenever you need it:

```
step: parse log line -> returns (level, service, message)
```

## Basics

### Define + call

```python
def greet(name):
    return f"hello {name}"

msg = greet("ops")
print(msg)
```

Explain:

- `def` defines a function
- `greet` is the function name
- `(name)` is a parameter (input)
- `return` sends a value back to the caller

### Print vs return

```python
def add(a, b):
    return a + b

print(add(2, 3))
```

If you only `print(...)` inside the function, you cannot use the value later.

## Hands-on Lab — Parse a simple log line

Create `parse_log.py`:

```python
def parse_kv_line(line):
    """Parse 'key=value' pairs separated by spaces into a dict."""
    result = {}
    for part in line.split():
        if "=" not in part:
            continue
        key, value = part.split("=", 1)
        result[key] = value
    return result


line = "ts=2026-03-15 level=ERROR service=api msg=timeout"
data = parse_kv_line(line)

print("service:", data.get("service"))
print("level:", data.get("level"))
print("msg:", data.get("msg"))
```

Expected output:

```text
service: api
level: ERROR
msg: timeout
```

## Common Mistakes (With Errors)

### Mistake 1 — Forgetting to call the function

Bad:

```python
def hello():
    return "hi"

print(hello)
```

This prints the function object, not the result.

### Mistake 2 — Missing required arguments

Bad:

```python
def add(a, b):
    return a + b

add(1)
```

Typical error:

```text
TypeError: add() missing 1 required positional argument: 'b'
```

### Mistake 3 — Returning vs printing confusion

Bad:

```python
def add(a, b):
    print(a + b)

total = add(1, 2)
print(total)
```

Expected behavior? You might expect `total` to be 3.

Reality: `total` becomes `None`.

## Quick Reference

- Define: `def name(params):`
- Return: `return value`
- If a function has no `return`, it returns `None`
- Docstring: first string inside function (triple quotes) describes behavior

## Next

Next: [Lesson 15 — Lists, Tuples, Sets](15-lists-tuples-sets.md)
