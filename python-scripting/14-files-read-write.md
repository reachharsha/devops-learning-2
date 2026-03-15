---
title: "Python Scripting: 14 - Files: Read/Write"
render_with_liquid: false
---

# Lesson 14 — Files: Read/Write

## Objectives

- Read text files
- Write text files
- Understand `with` blocks

## Concepts

### The `with` statement

`with` closes the file automatically.

```python
with open("file.txt", "r", encoding="utf-8") as f:
    data = f.read()
```

## Hands-on Lab

Create `files_demo.py`:

```python
path = "notes.txt"

with open(path, "w", encoding="utf-8") as f:
    f.write("line1\n")
    f.write("line2\n")

with open(path, "r", encoding="utf-8") as f:
    for line in f:
        print(line.strip())
```

## Quick Check

1) Why prefer `with open(...)`?
2) What does `encoding="utf-8"` do?

## Next

[Lesson 15: JSON/CSV/YAML Basics](15-json-csv-yaml.md)
