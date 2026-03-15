---
title: "Python for DevOps Automation: 29 - Advanced Files (glob, safe writes)"
render_with_liquid: false
---

# Lesson 29 — Advanced Files (glob, safe writes)

Real automation handles many files:

- rotating logs
- multiple configs
- reports per host

## Objectives

- Find files using glob patterns
- Walk directories recursively
- Write files safely (avoid partial writes)
- Understand `shutil` basics

## Mental Model

When you write a report, imagine a power outage mid-write.

- A safe write pattern avoids corrupting the old report.

## Glob patterns with `pathlib`

Create `list_logs.py`:

```python
from pathlib import Path

logs = Path("logs")

for p in logs.glob("*.log"):
    print(p)
```

Recursive:

```python
for p in logs.rglob("*.log"):
    print(p)
```

## Safe write pattern

Create `safe_write.py`:

```python
from pathlib import Path

target = Path("report.txt")
tmp = Path("report.txt.tmp")

tmp.write_text("status=OK\n", encoding="utf-8")
tmp.replace(target)  # atomic replace on most OS/filesystems

print("wrote safely")
```

## Copying files with `shutil`

```python
import shutil

shutil.copy2("report.txt", "report.bak.txt")
```

## Common Mistakes (With Errors)

### Mistake 1 — Using the wrong working directory

If `logs/` isn’t found:

```text
FileNotFoundError: ...
```

Fix: print `Path.cwd()` and adjust.

### Mistake 2 — Assuming `replace()` is always atomic

It’s usually atomic on the same filesystem.

Beginner rule: keep temp and target in the same folder.

## Quick Reference

- Glob: `Path("x").glob("*.log")`
- Recursive: `rglob("*.log")`
- Safe write: write temp → `replace()`
- Copy: `shutil.copy2(src, dst)`

## Next

Next: [Lesson 30 — Dataclasses & Type Hints](30-dataclasses-and-type-hints.md)
