---
title: "Python for DevOps Automation: 12 - Conditionals (if/elif/else)"
render_with_liquid: false
---

# Lesson 12 — Conditionals (if/elif/else)

Conditionals let your script **make decisions**.

In DevOps automation, this is the moment your script decides:

- “Is the service healthy?”
- “Should I retry?”
- “Is disk usage too high?”

## Objectives

By the end, you can:

- Write `if`, `elif`, `else` blocks correctly
- Read and fix common syntax/indentation errors
- Use comparisons (`==`, `!=`, `<`, `>`, `<=`, `>=`) and boolean logic (`and`, `or`, `not`)

## Mental Model (Analogy)

Think of `if/elif/else` like an **on-call runbook**:

```
IF impact is critical -> page immediately
ELIF impact is medium -> create ticket + notify
ELSE -> log it and continue
```

Your code becomes that runbook.

## Core Syntax

### `if` statement

```python
cpu = 92

if cpu > 90:
    print("CRIT: CPU is high")
```

Important pieces:

- `if` is a keyword: “start a decision.”
- The condition (`cpu > 90`) must evaluate to `True` or `False`.
- The `:` (colon) is required.
- The next lines must be **indented** (usually 4 spaces).

### `elif` and `else`

```python
usage = 78

if usage >= 90:
    print("CRIT")
elif usage >= 80:
    print("WARN")
else:
    print("OK")
```

## Boolean Logic

```python
is_prod = True
has_deploy_window = False

if is_prod and not has_deploy_window:
    print("BLOCK: no deploy window")
```

Explain the operators:

- `and`: both sides must be `True`
- `or`: at least one side must be `True`
- `not`: flips `True` ↔ `False`

## Hands-on Lab 1 — Status code to alert level

Create `status_check.py`:

```python
status_text = input("Enter HTTP status code (e.g., 200, 404, 503): ").strip()

try:
    status = int(status_text)
except ValueError:
    print("ERROR: please enter a number")
    raise SystemExit(1)

if status >= 500:
    print("CRIT: server error")
elif status >= 400:
    print("WARN: client error")
elif status >= 200:
    print("OK")
else:
    print("INFO: unexpected status")
```

Example runs:

```text
Enter HTTP status code (e.g., 200, 404, 503): 200
OK
```

```text
Enter HTTP status code (e.g., 200, 404, 503): 503
CRIT: server error
```

## Hands-on Lab 2 — Disk usage guardrail

Create `disk_guard.py`:

```python
percent_text = input("Disk usage percent (0-100): ").strip()

try:
    percent = float(percent_text)
except ValueError:
    print("ERROR: enter a number")
    raise SystemExit(1)

if percent < 0 or percent > 100:
    print("ERROR: percent must be between 0 and 100")
    raise SystemExit(1)

if percent >= 95:
    print("CRIT: disk almost full")
elif percent >= 85:
    print("WARN: disk getting full")
else:
    print("OK")
```

## Common Mistakes (With Real Errors)

### Mistake 1 — Missing colon

Bad:

```python
if percent > 90
    print("high")
```

Typical error:

```text
  File "disk_guard.py", line 1
    if percent > 90
                   ^
SyntaxError: expected ':'
```

### Mistake 2 — Indentation

Bad:

```python
if True:
print("oops")
```

Typical error:

```text
IndentationError: expected an indented block
```

### Mistake 3 — Comparing strings vs numbers

Bad:

```python
percent = input("Percent: ")
if percent > 90:
    print("high")
```

Why it’s wrong: `percent` is a string; comparing string to number fails.

Typical error:

```text
TypeError: '>' not supported between instances of 'str' and 'int'
```

Fix: convert using `int(...)` or `float(...)`.

## Quick Reference

- `if CONDITION:` start decision
- `elif CONDITION:` else-if branch
- `else:` fallback branch
- Comparisons: `== != < > <= >=`
- Boolean: `and` / `or` / `not`
- Validate and convert user input early (`int()`, `float()`) 

## Next

Next: [Lesson 13 — Loops](13-loops.html)
