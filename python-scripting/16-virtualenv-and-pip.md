---
title: "Python Scripting: 16 - venv + pip"
render_with_liquid: false
---

# Lesson 16 — venv + pip

## Objectives

- Understand why virtual environments exist
- Create and activate a venv
- Install packages with pip

## Concepts

### Why virtual environments?

They keep dependencies for one project separate from others.

## Hands-on Lab

Create a new folder and enter it:

```bash
mkdir my-python-project
cd my-python-project
```

Create a venv:

```bash
python3 -m venv .venv
```

Activate it:

```bash
source .venv/bin/activate
```

Now install a package:

```bash
python -m pip install requests
python -c "import requests; print(requests.__version__)"
```

## Quick Check

1) What problem does a venv solve?
2) Why run `python -m pip` instead of `pip` sometimes?

## Next

[Lesson 17: Logging & Debugging](17-logging-and-debugging.md)
