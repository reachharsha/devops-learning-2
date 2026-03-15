---
title: "Python for DevOps Automation: 08 - Output, Input, Comments"
render_with_liquid: false
---

# Lesson 08 — Output, Input, Comments

## Objectives

By the end, you can:

- Use `print()` to produce clean, readable output
- Use `sep=` and `end=` when formatting output
- Use `input()` and explain why it always returns a string
- Convert input safely with `int()` / `float()`
- Use comments (`#`) to document your scripts

## `print()` — output to the terminal

`print()` shows output in the terminal.

```python
print("hello")
```

### Printing multiple values

```python
host = "web-01"
port = 443
print("host:", host, "port:", port)
```

### `sep=` (separator)

```python
print("a", "b", "c", sep="|")
```

Output:

```text
a|b|c
```

### `end=` (line ending)

Default `end` is a newline (`\n`).

```python
print("Downloading...", end="")
print("done")
```

Output:

```text
Downloading...done
```

## `input()` — read user input

`input()` pauses the script and returns what the user typed.

Important: `input()` always returns a **string** (`str`).

Why: keyboard input is text; Python won’t guess the type.

So for numbers, you must convert.

## Type conversion

- `int("80")` → `80`
- `float("0.75")` → `0.75`

If conversion fails, Python raises `ValueError`.

## Comments

Comments start with `#` and are ignored by Python.

```python
# disk threshold used for alerts
threshold = 80
```

Comments help your future self (and teammates) understand intent.

## Hands-on Lab

Create `disk_threshold.py`:

```python
value_text = input("Enter disk usage percent (0-100): ")

try:
    value = int(value_text)
except ValueError:
    print("ERROR: enter a number like 80")
    raise SystemExit(1)

if value >= 80:
    print("ALERT: disk usage high")
else:
    print("OK: disk usage normal")
```

## Extra mini-lab — Clean output with f-strings

Create `format_output.py`:

```python
host = "web-01"
latency_ms = 12.3456

print(f"host={host} latency_ms={latency_ms:.2f}")
```

Expected output:

```text
host=web-01 latency_ms=12.35
```

## Common mistakes

### Mistake 1 — Doing math with strings

Bad:

```python
text = input("Retries: ")
print(text + 1)
```

Typical error:

```text
TypeError: can only concatenate str (not "int") to str
```

Fix: `int(text)` or `float(text)`.

### Mistake 2 — Not stripping input

Use `.strip()` to remove trailing spaces/newlines:

```python
value_text = input("Percent: ").strip()
```

## DevOps use case

Automation scripts need:

- clear output for humans/logs
- safe conversion and validation for inputs

## Quick Reference

- Print: `print(a, b, sep="-", end="\n")`
- Input: `text = input("...")`
- Convert: `int(text)` / `float(text)`
- Comment: `# explanation`

## Next

[Lesson 09: Operators & Type Conversion](09-operators-and-conversions.md)
