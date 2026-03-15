---
title: "Python Scripting: 07 - Conditionals (if/elif/else)"
render_with_liquid: false
---

# Lesson 07 — Conditionals (if/elif/else)

## Objectives

- Make decisions with `if`
- Add more branches with `elif`
- Handle the default case with `else`

## Concepts

Python uses **indentation** (spaces) to define blocks.

```python
if condition:
    # block
    pass
```

## Hands-on Lab

Create `grade.py`:

```python
score = 78

if score >= 90:
    print("A")
elif score >= 80:
    print("B")
elif score >= 70:
    print("C")
else:
    print("Needs improvement")
```

Change `score` and run again.

## Quick Check

1) Why does indentation matter?
2) What runs when no `if`/`elif` condition matches?

## Next

[Lesson 08: Loops (for/while)](08-loops.md)
