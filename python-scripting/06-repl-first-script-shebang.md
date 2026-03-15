---
title: "Python for DevOps Automation: 06 - REPL, First Script, Shebang"
render_with_liquid: false
---

# Lesson 06 — REPL, First Script, Shebang

## Objectives

By the end, you can:

- Explain what the REPL is (and when to use it)
- Run Python code as a script (`python3 file.py`)
- Understand what the shebang line does (`#!/usr/bin/env python3`)
- Make a script executable (`chmod +x`) and run it like a command (`./file.py`)

## Mental model

- REPL = a **practice area** (try small things quickly)
- Script = a **repeatable recipe** (run the same steps every time)

## REPL (Read–Eval–Print Loop)

REPL means:

- **Read** what you type
- **Eval** (run) it
- **Print** the result (or error)
- **Loop** back for the next line

Start the REPL:

```bash
python3
```

You’ll see a prompt like `>>>`.

Try a few safe experiments:

```python
>>> 2 + 2
4
>>> hostname = "web-01"
>>> hostname
'web-01'
>>> type(hostname)
<class 'str'>
```

Exit the REPL:

```python
>>> exit()
```

You can also press `Ctrl+D` on Linux/macOS.

## Script mode (a `.py` file)

A script is a Python file you can run again and again.

Run it like this:

```bash
python3 file.py
```

This is what you’ll do in CI, cron, and automation jobs.

## Shebang (the `#!` line)

If you want to run your script like a command (`./healthcheck.py`), you need a shebang.

Example:

```text
#!/usr/bin/env python3
```

What it means:

- `#!` tells the OS: “use the following program to run this file”
- `/usr/bin/env` looks up `python3` using your `PATH`
- `python3` is the interpreter

Why `/usr/bin/env python3`?

- It’s portable. Different machines can have `python3` in different locations.

## Hands-on Lab

Create `healthcheck.py`:

```python
#!/usr/bin/env python3

print("OK: script started")
```

Run:

```bash
python3 healthcheck.py
chmod +x healthcheck.py
./healthcheck.py
```

Expected output:

```text
OK: script started
```

## Common mistakes

### Mistake 1 — Permission denied

Typical error:

```text
zsh: permission denied: ./healthcheck.py
```

Fix:

```bash
chmod +x healthcheck.py
```

### Mistake 2 — Missing shebang when using `./file.py`

If the OS doesn’t know how to run the file, it may fail.

Fix: add a correct shebang OR run with `python3 file.py`.

### Mistake 3 — Running the wrong Python

If you have multiple Pythons installed, verify the one you are running:

```bash
which python3
python3 -V
```

## DevOps use case

Executable scripts are easy to run from cron and CI.

## Quick Reference

- REPL: `python3`
- Run: `python3 file.py`
- Executable: `chmod +x file.py` then `./file.py`
- Shebang: `#!/usr/bin/env python3`

## Next

[Lesson 07: Variables & Data Types](07-variables-and-types.md)
