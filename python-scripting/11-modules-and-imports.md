---
title: "Python Scripting: 11 - Modules & Imports"
render_with_liquid: false
---

# Lesson 11 — Modules & Imports

## Objectives

- Import standard library modules
- Import your own code
- Understand `if __name__ == "__main__":`

## Concepts

### Import standard library

```python
import os
import sys
```

### Import a function from a module

```python
from pathlib import Path
```

### Main guard

This is common in scripts:

```python
def main():
    print("running")

if __name__ == "__main__":
    main()
```

## Hands-on Lab

Create `main_demo.py`:

```python
from pathlib import Path

def main():
    here = Path(".").resolve()
    print(f"Current folder: {here}")

if __name__ == "__main__":
    main()
```

Run:

```bash
python3 main_demo.py
```

## Quick Check

1) What is the “standard library”?
2) Why use the main guard?

## Next

[Lesson 12: Errors & Exceptions](12-errors-and-exceptions.md)
