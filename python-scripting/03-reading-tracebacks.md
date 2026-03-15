---
title: "Python for DevOps Automation: 03 - Reading Tracebacks (Errors)"
render_with_liquid: false
---

# Lesson 03 — Reading Tracebacks (Errors)

## Objectives

- Understand what a traceback is
- Read tracebacks **bottom to top**
- Use file + line number to fix errors

## Real-world analogy

A traceback is a crash report that says:

- where the crash happened
- what kind of crash it was
- why it crashed

## Concepts
## What is a traceback?

A traceback is Python’s “what just happened” report when your program crashes.

It usually contains:

- which file crashed
- which line crashed
- which function it was in
- the exception type (`NameError`, `TypeError`, etc.)
- a message that explains the failure

### Read bottom to top

Bottom line is usually the real reason.

## The call stack (why there are multiple lines)

If function A calls function B, and B crashes, Python shows both.

Think: “How did we get here?”

```
main() -> parse_line() -> to_int()  X crash here
```

The traceback prints that stack so you can follow the path.

## How to read a traceback (practical steps)

1) Go to the **last line** (exception type + message)
2) Then look for the last `File "...", line N` entry
3) Open that file and go to line N
4) Fix the *real* cause (often wrong type, missing key, bad input)

## Hands-on Lab

Create `broken_log_parser.py`:

```python
log_line = "ERROR disk full on /var"

print("Parsing...")
print(level)  # level is not defined
```

Run:

```bash
python3 broken_log_parser.py
```

You should see something like:

```text
NameError: name 'level' is not defined
```

Fix it:

```python
log_line = "ERROR disk full on /var"

print("Parsing...")
level = log_line.split()[0]
print("level:", level)
```

Expected output:

```text
Parsing...
level: ERROR
```

## Hands-on Lab 2 — Multi-line traceback (call stack)

Create `stack_demo.py`:

```python
def parse_retries(text):
	return int(text)


def load_settings():
	# imagine this came from an env var or config file
	retries_text = "three"
	return {"retries": parse_retries(retries_text)}


settings = load_settings()
print(settings)
```

Run:

```bash
python3 stack_demo.py
```

You’ll see a traceback that includes multiple frames, ending with something like:

```text
ValueError: invalid literal for int() with base 10: 'three'
```

Read it bottom-to-top:

- bottom says `ValueError` from `int(text)`
- above shows it happened inside `parse_retries`
- above shows `load_settings` passed in a bad string

Fix: change `retries_text` to `"3"` or add error handling with `try/except`.

## Common mistakes

### Mistake 1 — Only reading the first line

The first line says “Traceback (most recent call last)”.

It’s not the cause.

### Mistake 2 — Ignoring the exception type

The exception type often tells you exactly what class of bug it is:

- `NameError`: you used a variable name that doesn’t exist
- `TypeError`: you used the wrong type (like adding a string to a number)
- `ValueError`: correct type, but invalid value (like `int("abc")`)
- `KeyError`: missing dict key
- `IndexError`: list index out of range

### Mistake 3 — Fixing the symptom, not the cause

If you see `TypeError`, fix the type conversion. Don’t just delete lines until it stops.

## DevOps use case

Debugging is daily work. Tracebacks are your fastest feedback loop.

## Quick Reference

- Traceback = crash report
- Read bottom to top
- Focus on: file + line + error type + message
- Multiple "File ..." lines = call stack (who called who)

## Next

[Lesson 04: Install Python on Linux](04-install-python-linux.md)
