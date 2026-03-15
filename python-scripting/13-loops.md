---
title: "Python for DevOps Automation: 13 - Loops (for/while)"
render_with_liquid: false
---

# Lesson 13 — Loops (for/while)

Loops let you repeat work safely and consistently.

In DevOps, that often means:

- iterate servers
- scan log lines
- retry flaky operations (with limits)

## Objectives

- Use `for` loops to iterate lists and strings
- Use `while` loops for retries and “until” conditions
- Understand `break` and `continue`
- Avoid infinite loops

## Mental Model (Analogy)

Think of a loop as a **checklist**.

You don’t want to “remember” steps. You want to run the same steps for each item:

```
for each server:
  check health
  record result
```

## `for` loops

### Loop over a list

```python
servers = ["web-01", "web-02", "api-01"]

for server in servers:
    print("checking", server)
```

Explain keywords:

- `for` starts the loop
- `server` is a variable that takes each value one-by-one
- `in` means “take items from this collection”

### Loop over a range of numbers

```python
for attempt in range(1, 4):
    print("attempt", attempt)
```

`range(1, 4)` produces 1, 2, 3 (the end is **not included**).

## `while` loops

Use `while` when you don’t know the number of iterations up front.

```python
attempt = 1

while attempt <= 3:
    print("attempt", attempt)
    attempt += 1
```

`attempt += 1` means “increase attempt by 1”.

## `break` and `continue`

- `break` exits the loop immediately
- `continue` skips to the next iteration

```python
for line in ["OK", "OK", "ERROR", "OK"]:
    if line == "ERROR":
        print("found error, stopping")
        break
    print("line was", line)
```

## Hands-on Lab 1 — Count errors in logs

Create `count_errors.py`:

```python
log_text = """\
2026-03-15T10:00:00Z INFO service=api msg=started
2026-03-15T10:00:01Z ERROR service=api msg=timeout
2026-03-15T10:00:02Z INFO service=api msg=retry
2026-03-15T10:00:03Z ERROR service=api msg=timeout
"""

error_count = 0

for line in log_text.splitlines():
    line = line.strip()
    if not line:
        continue
    if " ERROR " in line:
        error_count += 1

print("errors:", error_count)
```

Expected output:

```text
errors: 2
```

## Hands-on Lab 2 — Retry loop (safe)

Create `retry_sim.py`:

```python
max_attempts = 3
attempt = 1

while attempt <= max_attempts:
    answer = input(f"Attempt {attempt}/{max_attempts}. Type 'ok' to succeed: ").strip().lower()

    if answer == "ok":
        print("SUCCESS")
        break

    print("not ok, retrying...")
    attempt += 1
else:
    # This else belongs to the while-loop (not the if)
    print("FAILED: max attempts reached")
```

Note: The `else:` here runs only if the loop did **not** hit `break`.

## Common Mistakes

### Mistake 1 — Infinite loop

Bad:

```python
while True:
    print("running")
```

Fix: add a stop condition or `break`.

### Mistake 2 — Off-by-one in `range`

If you want 3 tries, use `range(1, 4)` or `range(3)`.

### Mistake 3 — Modifying a variable but forgetting `+= 1`

Bad:

```python
attempt = 1
while attempt <= 3:
    print(attempt)
    # forgot attempt += 1
```

## Quick Reference

- `for x in items:` iterate items
- `range(n)` gives 0..n-1
- `while condition:` keep looping while condition is True
- `break` stops the loop
- `continue` skips to next iteration

## Next

Next: [Lesson 14 — Functions](14-functions.html)
