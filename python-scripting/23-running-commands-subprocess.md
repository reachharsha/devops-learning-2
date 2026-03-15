---
title: "Python for DevOps Automation: 23 - Running Commands (subprocess)"
render_with_liquid: false
---

# Lesson 23 — Running Commands (`subprocess`)

Many automation tasks call system commands:

- `df -h` (disk)
- `systemctl status ...`
- `kubectl get pods`

Python can run commands and capture output using `subprocess`.

## Objectives

- Run a command safely (no shell injection)
- Capture output (stdout/stderr)
- Detect failures using exit codes
- Use timeouts

## Mental Model

`subprocess` is like hiring a temporary worker:

- you give the command
- you get back output + exit status

## Recommended pattern: `subprocess.run([...], check=True)`

Create `run_df.py`:

```python
import subprocess

result = subprocess.run(
    ["df", "-h"],
    text=True,
    capture_output=True,
    check=True,
)

print("exit:", result.returncode)
print("stdout:\n", result.stdout)
```

Notes:

- command is a list: `["df", "-h"]` (safer)
- `text=True` gives you strings, not bytes
- `capture_output=True` captures stdout/stderr
- `check=True` raises an error if exit code is non-zero

## Handling failures

Create `run_command_safe.py`:

```python
import subprocess

try:
    subprocess.run(["false"], check=True)
except subprocess.CalledProcessError as e:
    print("command failed")
    print("exit:", e.returncode)
    raise SystemExit(1)
```

Expected output:

```text
command failed
exit: 1
```

## Timeouts

```python
import subprocess

try:
    subprocess.run(["sleep", "10"], timeout=1)
except subprocess.TimeoutExpired:
    print("timeout")
```

## Common Mistakes (With Errors)

### Mistake 1 — Using `shell=True` without understanding

Avoid unless you really need shell features.

Bad (dangerous if user-controlled input is included):

```python
subprocess.run("df -h", shell=True)
```

Better:

```python
subprocess.run(["df", "-h"])
```

### Mistake 2 — Not capturing stderr

If a command fails, stderr often contains the real clue.

Fix: use `capture_output=True` and print `result.stderr`.

## Quick Reference

- Run: `subprocess.run(["cmd", "arg"], check=True, text=True, capture_output=True)`
- Failure: `subprocess.CalledProcessError`
- Timeout: `timeout=5` → `subprocess.TimeoutExpired`

## Next

Next: [Lesson 24 — Logging (instead of print)](24-logging-basics.md)
