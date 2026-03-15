---
title: "Python Scripting: 19 - subprocess & Shell Commands"
render_with_liquid: false
---

# Lesson 19 — subprocess & Shell Commands

## Objectives

- Run a command from Python
- Capture stdout/stderr
- Learn safe patterns for automation

## Concepts

### Why `subprocess`?

DevOps scripts often call tools like `git`, `docker`, `kubectl`.

### Prefer “list args” (safer)

```python
import subprocess

result = subprocess.run(["echo", "hello"], capture_output=True, text=True)
```

## Hands-on Lab

Create `subprocess_demo.py`:

```python
import subprocess

result = subprocess.run(
    ["python3", "--version"],
    capture_output=True,
    text=True,
)

print("exit:", result.returncode)
print("stdout:", result.stdout.strip())
print("stderr:", result.stderr.strip())
```

## Quick Check

1) What is `returncode`?
2) Why avoid `shell=True` as a beginner default?

## Next

[Lesson 20: Regex & Text Processing](20-regex-and-text-processing.md)
