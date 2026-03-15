---
title: "Python Scripting: 13 - Paths with pathlib"
render_with_liquid: false
---

# Lesson 13 — Paths with pathlib

## Objectives

- Build file paths safely
- Check if files/folders exist
- List files in a folder

## Concepts

### Why `pathlib`?

Paths differ across OS (macOS/Linux/Windows). `pathlib` helps you write portable scripts.

```python
from pathlib import Path

p = Path("logs") / "app.log"
```

## Hands-on Lab

Create `paths_demo.py`:

```python
from pathlib import Path

root = Path(".").resolve()
print(f"Root: {root}")

for child in root.iterdir():
    print(child.name, "dir" if child.is_dir() else "file")
```

## Quick Check

1) What does `Path(".")` mean?
2) How do you join paths with `pathlib`?

## Next

[Lesson 14: Files (Read/Write)](14-files-read-write.md)
