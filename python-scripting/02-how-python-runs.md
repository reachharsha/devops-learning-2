---
title: "Python Scripting: 02 - How Python Runs"
render_with_liquid: false
---

# Lesson 02 — How Python Runs

## Objectives

- Understand scripts vs the interactive shell (REPL)
- Learn what the interpreter does
- Know where errors show up

## Concepts

### Interpreter

`python3` is the **interpreter**. It reads your code and executes it.

### Script mode

You run a file:

```bash
python3 my_script.py
```

### Interactive mode (REPL)

You can try quick experiments:

```bash
python3
```

Then type:

```python
2 + 2
print("hi")
```

Exit with:

```python
exit()
```

### Errors and “tracebacks”

When something breaks, Python prints a **traceback**. It tells you:

- what file
- what line
- what error

## Hands-on Lab

Create `broken.py`:

```python
print("Start")
print(1 / 0)
print("End")
```

Run:

```bash
python3 broken.py
```

Observe:

- `Start` prints
- then you get `ZeroDivisionError`
- `End` never runs

## Quick Check

1) What is the REPL?
2) What is a traceback?
3) Why didn’t `End` print?

## Next

[Lesson 03: Variables & Types](03-variables-and-types.md)
