---
title: "Python Scripting: 32 - Packaging & Project Layout"
render_with_liquid: false
---

# Lesson 32 — Packaging & Project Layout

## Objectives

- Learn a clean project layout
- Understand `pyproject.toml` at a high level
- Prepare scripts to be shared/reused

## Concepts

When your script becomes important, you want:

- repeatable installs
- pinned dependencies
- tests

## Hands-on Lab

Recommended simple layout:

```text
mytool/
  src/mytool/__init__.py
  src/mytool/cli.py
  tests/
  pyproject.toml
  README.md
```

You can start small, and grow into this later.

## Quick Check

1) Why is a standard layout helpful?
2) What problem does packaging solve?

## Next

[Lesson 33: HTTP Retries & Resilience](33-http-retries-and-resilience.md)
