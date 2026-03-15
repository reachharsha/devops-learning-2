---
title: "Python Scripting: 31 - OOP for Automation"
render_with_liquid: false
---

# Lesson 31 — OOP for Automation

## Objectives

- Organize scripts into small, testable components
- Separate “logic” from “I/O”
- Make your code easier to extend

## Concepts

A common pattern:

- parse inputs (CLI/env)
- run logic
- print results

Keep network calls and file I/O in small functions so they can be tested/mocked.

## Hands-on Lab

Create `service_demo.py`:

```python
class Calculator:
    def add(self, a, b):
        return a + b


def main():
    calc = Calculator()
    print(calc.add(10, 5))


if __name__ == "__main__":
    main()
```

## Quick Check

1) Why separate I/O from logic?
2) How does this help testing?

## Next

[Lesson 32: Packaging & Project Layout](32-packaging-and-project-layout.md)
