---
title: "Python Scripting: 01 - Install Python & Tools"
render_with_liquid: false
---

# Lesson 01 — Install Python & Tools

## Objectives

- Install Python 3 safely
- Verify it works from the terminal
- Set up a code editor (VS Code)

## Concepts

### What is Python?

Python is a programming language. For scripting, you write a `.py` file and run it with the `python3` command.

### “Python 3” vs “Python”

- You want **Python 3**.
- On some systems, `python` may point to Python 2 (old) or not exist.

## Hands-on Lab

### Step 1: Check if Python is already installed

Run:

```bash
python3 --version
```

If you see something like `Python 3.x.y`, you’re good.

### Step 2: Install Python (macOS)

Two common options:

1) **Official installer** (python.org)
2) **Homebrew** (popular on macOS)

If you already use Homebrew:

```bash
brew install python
python3 --version
```

### Step 3: Install VS Code

- Install VS Code
- Install the **Python** extension (Microsoft)

### Step 4: Write your first program

Create a file named `hello.py`:

```python
print("Hello, world!")
```

Run it:

```bash
python3 hello.py
```

## Quick Check

1) What command prints your Python version?
2) What file extension is a Python script?
3) What command runs a Python script file?

## Next

[Lesson 02: How Python Runs](02-how-python-runs.md)
