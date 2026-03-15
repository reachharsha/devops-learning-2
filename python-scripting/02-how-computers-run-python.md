---
title: "Python for DevOps Automation: 02 - How Computers Run Python"
render_with_liquid: false
---

# Lesson 02 — How Computers Run Python

## Objectives

By the end, you can:

- Explain what “source code” is (`.py` files)
- Explain what the Python interpreter (`python3`) is
- Understand “compiled vs interpreted” as a spectrum
- Understand what bytecode and `__pycache__/` are (and why they exist)
- Know what actually happens when you run `python3 script.py`

## Real-world analogy

Two ways to deliver instructions:

1) **Interpreter**: translator translates line-by-line while you talk
2) **Compiler**: translate the whole book once, then reuse

Python feels “interpreter-style” as you learn.

## Big picture: what happens when you run a Python script?

When you run:

```bash
python3 script.py
```

your computer does roughly this:

```
you type command
   |
   v
OS starts the python3 program (a process)
   |
   v
python3 reads your script.py text
   |
   v
python3 parses it (checks syntax)
   |
   v
python3 compiles it to bytecode (internal)
   |
   v
python3 executes bytecode in the Python VM
   |
   v
your script prints output / writes files / calls APIs
```

Don’t worry about every step yet — the goal is to understand *why* some files appear and *why* some errors happen.

## Source code (`.py`)

### Source code

The `.py` file you write is **source code**: human-readable instructions.

Example:

```python
print("hello")
```

The computer does not directly execute the letters `p r i n t`.

It needs an interpreter.

## The interpreter (`python3`)

When you run:

```bash
python3 script.py
```

`python3` is a program (the **Python interpreter**) that reads your `.py` code and executes it.

### Interpreter vs compiler (beginner view)

- **Compiler**: translate the whole program first, then run the translated program.
- **Interpreter**: run the program through a runtime that reads/executes it.

Python uses both ideas:

- It *does* compile your code into **bytecode** (internal instructions)
- But you usually still run through the interpreter (`python3`), not a standalone binary

So it’s best to think: “Python is executed by an interpreter, but it also compiles to bytecode behind the scenes.”

## Bytecode and `__pycache__/`

Python often compiles your code into **bytecode** and may cache it as a `.pyc` file under `__pycache__/`.

Why cache?

- next run can start faster (Python can reuse cached bytecode)

Simple picture:

Simple picture:

```text
script.py  ->  python3  ->  runs
   |
   +--> __pycache__/ (cache)
```

You normally ignore `__pycache__`.

Important: `__pycache__/` is not “your source code”. It’s a cache.

## Hands-on Lab

Create `hello.py`:

```python
print("Hello from a DevOps automation script")
```

Run:

```bash
python3 hello.py
```

Expected output:

```text
Hello from a DevOps automation script
```

### Optional lab — See `__pycache__` appear

Create two files in the same folder.

Create `helper.py`:

```python
def banner(text):
   return f"=== {text} ==="
```

Create `main.py`:

```python
import helper

print(helper.banner("starting"))
```

Run:

```bash
python3 main.py
```

Now list the directory:

```bash
ls
```

You will often see a `__pycache__/` directory created.

## Common mistakes (and what they mean)

### Mistake 1 — Using `python` instead of `python3`

## Common mistakes

### Mistake: using `python` instead of `python3`

On some systems `python` may be missing or point elsewhere.

Fix: use `python3`.

### Mistake 2 — Running a script from the wrong folder

If you do:

```bash
python3 hello.py
```

but you’re not in the folder where `hello.py` exists, you’ll get:

```text
python3: can't open file 'hello.py': [Errno 2] No such file or directory
```

Fix: `cd` into the correct directory or use the correct path.

### Mistake 3 — Syntax errors happen before “running”

If your code has a syntax error (like a missing `)`), Python can’t even start executing it.

That’s why syntax errors feel immediate.

## DevOps use case

In CI/CD, you commonly:

- install python
- install dependencies
- run scripts

## Quick Reference

- `.py` = source code
- `python3` = interpreter
- `__pycache__/` = cache (ignore)
- “compiled vs interpreted” is a spectrum; Python compiles to bytecode but runs via the interpreter

## Next

[Lesson 03: Reading Tracebacks (Errors)](03-reading-tracebacks.md)
