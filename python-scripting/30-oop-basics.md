---
title: "Python Scripting: 30 - OOP (Basics)"
render_with_liquid: false
---

# Lesson 30 — OOP (Basics)

## Objectives

- Understand classes and objects
- Use methods
- Know when OOP helps scripting

## Concepts

OOP helps when scripts grow and you need to organize logic.

## Hands-on Lab

Create `oop_demo.py`:

```python
class Greeter:
    def __init__(self, prefix):
        self.prefix = prefix

    def greet(self, name):
        return f"{self.prefix} {name}"


g = Greeter(prefix="Hello")
print(g.greet("Alice"))
```

## Quick Check

1) What is `self`?
2) What is an object?

## Next

[Lesson 31: OOP for Automation](31-oop-for-automation.md)
