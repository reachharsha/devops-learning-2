---
title: "Python Scripting: 15 - JSON/CSV/YAML Basics"
render_with_liquid: false
---

# Lesson 15 — JSON/CSV/YAML Basics

## Objectives

- Read/write JSON using `json`
- Read/write CSV using `csv`
- Understand YAML (popular in DevOps)

## Concepts

### JSON

JSON is a text format for structured data.

### CSV

CSV is rows/columns, often used in exports.

### YAML

YAML is human-friendly config. Python needs a library (like `PyYAML`) to parse it.

## Hands-on Lab

### JSON example

Create `json_demo.py`:

```python
import json

data = {"name": "Alice", "skills": ["python", "devops"]}

text = json.dumps(data, indent=2)
print(text)

loaded = json.loads(text)
print(loaded["name"], loaded["skills"]) 
```

### CSV example

Create `csv_demo.py`:

```python
import csv

rows = [
    {"name": "Alice", "age": "30"},
    {"name": "Bob", "age": "25"},
]

with open("people.csv", "w", newline="", encoding="utf-8") as f:
    writer = csv.DictWriter(f, fieldnames=["name", "age"])
    writer.writeheader()
    writer.writerows(rows)

with open("people.csv", "r", encoding="utf-8") as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(row)
```

## Quick Check

1) Which module handles JSON in the standard library?
2) Why is YAML common in DevOps?

## Next

[Lesson 16: venv + pip](16-virtualenv-and-pip.md)
