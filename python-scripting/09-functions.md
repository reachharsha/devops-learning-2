---
title: "Python Scripting: 09 - Functions"
render_with_liquid: false
---

# Lesson 09 — Functions

## Objectives

- Define and call functions
- Use parameters and return values
- Understand scope (simple version)

## Concepts

Functions let you reuse code.

```python
def add(a, b):
    return a + b
```

## Hands-on Lab

Create `functions_demo.py`:

```python
def greet(name):
    return f"Hello, {name}!"

def add(a, b):
    return a + b

print(greet("Alice"))
print(add(10, 5))
```

Try changing inputs.

## Quick Check

1) What is the purpose of `return`?
2) What are parameters?

## Next

[Lesson 10: Collections (list/dict/set/tuple)](10-collections.md)
