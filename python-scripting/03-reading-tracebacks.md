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

Traceback contains:

- file name
- line number
- error type (example: `NameError`)
- error message

### Read bottom to top

Bottom line is usually the real reason.

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

## Common mistakes

- Only reading the first line
- Not noticing the line number

## DevOps use case

Debugging is daily work. Tracebacks are your fastest feedback loop.

## Quick Reference

- Traceback = crash report
- Read bottom to top
- Focus on: file + line + error type + message

## Next

[Lesson 04: Install Python on Linux](04-install-python-linux.md)
