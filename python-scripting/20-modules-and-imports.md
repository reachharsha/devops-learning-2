---
title: "Python for DevOps Automation: 20 - Modules & Imports"
render_with_liquid: false
---

# Lesson 20 — Modules & Imports

So far you’ve written **one-file scripts**.

In real DevOps automation, scripts grow. When a script grows, you need:

- reusable functions
- a clean structure
- a way to split code into multiple files

That’s exactly what **modules** and **imports** are for.

## Objectives

- Understand what a module is
- Import modules and functions safely
- Understand `__name__ == "__main__"`
- Create a small multi-file project
- Avoid common import errors

## Mental Model

Think of a module like a **toolbox**.

- A file like `utils.py` is a toolbox.
- Functions inside are tools.
- `import utils` is “bring the toolbox into the room”.

## What is a module?

A **module** is just a Python file (`.py`).

Example:

- `utils.py` is a module
- `check_disk.py` is a module

## What is a package?

A **package** is a folder of Python modules.

Common modern Python packages use:

- a folder like `mytool/`
- an `__init__.py` file (sometimes optional in newer Python, but still common)

For now, we’ll keep it simple with two files in one folder.

## Import styles

### 1) Import the whole module

```python
import math
print(math.sqrt(9))
```

### 2) Import a specific name

```python
from math import sqrt
print(sqrt(9))
```

Beginner rule:

- Prefer `import module` when you’re learning (clearer)
- Use `from module import name` when it improves readability

## `__name__` and "main"

When Python runs a file directly, it sets:

- `__name__ == "__main__"`

When Python imports a file, it sets:

- `__name__ == "module_name"`

This lets you write code that can be:

- imported safely (doesn’t auto-run)
- executed as a script when needed

Pattern:

```python
def main():
    print("hello")


if __name__ == "__main__":
    main()
```

## Hands-on Lab — Split a script into two files

Create a folder (example): `mini_project/`

Inside it, create `helpers.py`:

```python
def is_threshold_breached(value, threshold):
    return value >= threshold
```

Now create `check_cpu.py`:

```python
import helpers


def main():
    cpu = 91
    threshold = 90

    if helpers.is_threshold_breached(cpu, threshold):
        print("ALERT: cpu high")
    else:
        print("OK")


if __name__ == "__main__":
    main()
```

Run it:

```bash
python3 check_cpu.py
```

Expected output:

```text
ALERT: cpu high
```

## Common Mistakes (With Errors)

### Mistake 1 — `ModuleNotFoundError`

Typical error:

```text
ModuleNotFoundError: No module named 'helpers'
```

Common causes:

- You ran the script from the wrong folder
- The file name is different (`helper.py` vs `helpers.py`)

Fix:

- `cd` into the folder that contains the files and run from there
- or use a proper package structure later

### Mistake 2 — Importing runs code unintentionally

If `helpers.py` contains top-level code like `print("hi")`, it will run on import.

Fix: put runnable code into a `main()` function and guard it with:

```python
if __name__ == "__main__":
    main()
```

## Quick Reference

- Module = a `.py` file
- Package = a folder of modules
- Import:
  - `import module`
  - `from module import name`
- Main guard:
  - `if __name__ == "__main__":`

## Next

Next: [Lesson 21 — Command-Line Arguments (argparse)](21-command-line-arguments-argparse.md)
