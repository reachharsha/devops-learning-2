---
title: "Python for DevOps Automation: 02 - How Computers Run Python"
render_with_liquid: false
---

# Lesson 02 — How Computers Run Python

## Objectives

- Understand compilation vs interpretation
- Understand what the Python interpreter is
- Understand source code vs bytecode
- Know what `.py` files are

## Real-world analogy

Two ways to deliver instructions:

1) **Interpreter**: translator translates line-by-line while you talk
2) **Compiler**: translate the whole book once, then reuse

Python feels “interpreter-style” as you learn.

## Concepts

### Source code

The `.py` file you write is source code.

### The interpreter

When you run:

```bash
python3 script.py
```

`python3` is a program that reads your code and executes it.

### Bytecode and `__pycache__`

Python may create cached bytecode (`.pyc`) inside `__pycache__/`.

Simple picture:

```text
script.py  ->  python3  ->  runs
   |
   +--> __pycache__/ (cache)
```

You normally ignore `__pycache__`.

## Hands-on Lab

Create `hello.py`:

```python
print("Hello from a DevOps automation script")
```

Run:

```bash
python3 hello.py
```

Expected output:

```text
Hello from a DevOps automation script
```

## Common mistakes

### Mistake: using `python` instead of `python3`

On some systems `python` may be missing or point elsewhere.

Fix: use `python3`.

## DevOps use case

In CI/CD, you commonly:

- install python
- install dependencies
- run scripts

## Quick Reference

- `.py` = source code
- `python3` = interpreter
- `__pycache__/` = cache (ignore)

## Next

[Lesson 03: Reading Tracebacks (Errors)](03-reading-tracebacks.md)
