---
title: "Python Scripting: 08 - Loops (for/while)"
render_with_liquid: false
---

# Lesson 08 — Loops (for/while)

## Objectives

- Repeat work using loops
- Use `for` with `range()`
- Use `while` carefully

## Concepts

### for loop

```python
for i in range(3):
    print(i)
```

### while loop

```python
count = 0
while count < 3:
    print(count)
    count += 1
```

## Hands-on Lab

Create `loops_demo.py`:

```python
for i in range(1, 6):
    print(f"Number: {i}")

print("---")

count = 3
while count > 0:
    print(f"Countdown: {count}")
    count -= 1

print("Done")
```

## Quick Check

1) What does `range(1, 6)` produce?
2) What mistake can cause an infinite `while` loop?

## Next

[Lesson 09: Functions](09-functions.md)
