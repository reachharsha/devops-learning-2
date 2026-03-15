---
title: "Python for DevOps Automation: 27 - CSV (read/write)"
render_with_liquid: false
---

# Lesson 27 — CSV (Read/Write)

CSV is a very common “simple spreadsheet” format.

DevOps use cases:

- exporting reports
- importing inventory lists

## Objectives

- Read CSV using `csv.DictReader`
- Write CSV using `csv.DictWriter`
- Understand headers and rows
- Avoid common newline/format mistakes

## Mental Model

CSV is like a table:

- first line is column names (headers)
- each next line is a row

## Read CSV

Create `inventory.csv`:

```csv
host,env,ip
web-01,prod,10.0.0.10
api-01,stage,10.0.1.10
```

Create `read_inventory_csv.py`:

```python
import csv

with open("inventory.csv", "r", encoding="utf-8", newline="") as f:
    reader = csv.DictReader(f)
    for row in reader:
        print("host:", row["host"], "env:", row["env"], "ip:", row["ip"])
```

Expected output:

```text
host: web-01 env: prod ip: 10.0.0.10
host: api-01 env: stage ip: 10.0.1.10
```

## Write CSV

Create `write_report_csv.py`:

```python
import csv

rows = [
    {"service": "api", "healthy": "yes"},
    {"service": "worker", "healthy": "no"},
]

with open("report.csv", "w", encoding="utf-8", newline="") as f:
    writer = csv.DictWriter(f, fieldnames=["service", "healthy"])
    writer.writeheader()
    writer.writerows(rows)

print("wrote report.csv")
```

## Common Mistakes (With Errors)

### Mistake 1 — Forgetting headers

If you try to read without correct headers, you’ll get missing keys:

```text
KeyError: 'host'
```

Fix: ensure the first row has the right column names.

### Mistake 2 — Newline issues on some systems

Beginner rule: when using `csv`, pass `newline=""` to `open()`.

## Quick Reference

- Read: `csv.DictReader(file)`
- Write: `csv.DictWriter(file, fieldnames=[...])`
- `writer.writeheader()`
- `writer.writerows(rows)`

## Next

Next: [Lesson 28 — HTTP APIs (requests)](28-http-apis-requests.md)
