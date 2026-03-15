---
title: "Python Scripting: 35 - Mini Capstone"
render_with_liquid: false
---

# Lesson 35 — Mini Capstone: Log Scanner CLI

## Objectives

- Combine: argparse + files + regex + logging
- Build a real automation-style tool
- Produce a useful output summary

## Project

Write a CLI tool that scans a log file and counts:

- number of ERROR lines
- number of WARNING lines
- unique IPs found in the file

## Suggested steps

1) Create `scan_logs.py` with `argparse`:
   - required argument: `path`
2) Read the file line-by-line
3) If line contains `ERROR` / `WARNING`, increment counters
4) Use a regex to extract IPs and store in a set
5) Print a summary

## Regex hint (IP)

```python
r"\b(?:\d{1,3}\.){3}\d{1,3}\b"
```

## Quick Check

1) Why read line-by-line for large files?
2) Why use a set for unique IPs?

## Next

Next batch will go deeper into packaging, async, performance, and bigger capstones.
