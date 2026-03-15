---
title: "Python for DevOps Automation: 17 - Files & Paths (pathlib)"
render_with_liquid: false
---

# Lesson 17 — Files & Paths (`pathlib`)

Automation usually means reading and writing files:

- parse logs
- read config
- write reports

This lesson uses `pathlib` (modern, readable path handling).

## Objectives

- Read a text file safely
- Write an output file
- Understand paths, relative vs absolute
- Avoid common “file not found” problems
- Use `with` to open files safely
- Read large files line-by-line (log parsing)

## Mental Model (Analogy)

Files are like **documents in a filing cabinet**.

- The *path* is the cabinet → drawer → folder chain.
- Your script’s working directory is “where you are standing”.

## Relative vs absolute paths

- Relative path: `sample.log` (relative to the current working directory)
- Absolute path: `/var/log/syslog` (full location)

You can check your current working directory:

```python
import os
print(os.getcwd())
```

## Reading a file

Create a sample file `sample.log`:

```text
INFO started
ERROR timeout
INFO retry
```

Now create `read_log.py`:

```python
from pathlib import Path

path = Path("sample.log")

if not path.exists():
    print("ERROR: file not found:", path)
    raise SystemExit(1)

text = path.read_text(encoding="utf-8")

error_count = 0
for line in text.splitlines():
    if line.startswith("ERROR"):
        error_count += 1

print("errors:", error_count)
```

Expected output:

```text
errors: 1
```

## Writing a report

Create `write_report.py`:

```python
from pathlib import Path

report = Path("report.txt")
report.write_text("status=OK\n", encoding="utf-8")
print("wrote:", report)
```

Expected output:

```text
wrote: report.txt
```

## The `with open(...)` pattern (recommended)

`path.read_text()` is convenient, but for larger files and streaming you’ll often use `with`.

Create `read_log_stream.py`:

```python
from pathlib import Path

path = Path("sample.log")

error_count = 0
with path.open("r", encoding="utf-8") as f:
    for line in f:
        line = line.strip()
        if line.startswith("ERROR"):
            error_count += 1

print("errors:", error_count)
```

Why `with` matters:

- it closes the file automatically
- it’s safer (no forgotten `close()`)

## Create directories and list files

```python
from pathlib import Path

out_dir = Path("out")
out_dir.mkdir(exist_ok=True)

for p in out_dir.iterdir():
    print("found:", p)
```

## Common Mistakes (With Errors)

### Mistake 1 — Wrong working directory

If your script can’t find `sample.log`, you may be running it from a different folder.

Tip: print your current folder:

```python
import os
print(os.getcwd())
```

### Mistake 2 — Permission denied

If you try to write into a protected folder (like `/root/`), you might see:

```text
PermissionError: [Errno 13] Permission denied
```

Fix: write into a folder you own, or run with the correct permissions (carefully).

### Mistake 3 — FileNotFoundError

Typical error:

```text
FileNotFoundError: [Errno 2] No such file or directory: 'sample.log'
```

Fix: confirm the file exists, or use the correct path.

### Mistake 4 — Encoding problems

If you read a file with the wrong encoding you may get a `UnicodeDecodeError`.

Fix: use `encoding="utf-8"` (common) or detect/handle encoding properly.

## Quick Reference

- `from pathlib import Path`
- `Path("file.txt")` creates a path object
- `path.exists()` checks existence
- `path.read_text(encoding="utf-8")`
- `path.write_text("...", encoding="utf-8")`
- Stream read: `with Path("x").open() as f: ...`
- Make directory: `Path("out").mkdir(exist_ok=True)`

## Next

Next: [Lesson 18 — JSON & YAML Config](18-json-yaml-config.md)

