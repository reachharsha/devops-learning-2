---
title: "Python Scripting: 18 - Build a CLI with argparse"
render_with_liquid: false
---

# Lesson 18 — Build a CLI with argparse

## Objectives

- Accept input from the command line
- Provide `--help`
- Build small tools you can reuse

## Concepts

### Why CLI tools?

In DevOps, most automation is command-driven.

## Hands-on Lab

Create `hello_cli.py`:

```python
import argparse

def main():
    parser = argparse.ArgumentParser(description="Say hello")
    parser.add_argument("name", help="Name to greet")
    args = parser.parse_args()

    print(f"Hello, {args.name}!")

if __name__ == "__main__":
    main()
```

Run:

```bash
python3 hello_cli.py --help
python3 hello_cli.py Alice
```

## Quick Check

1) What does `--help` do?
2) Where do parsed arguments appear?

## Next

[Lesson 19: subprocess & Shell Commands](19-subprocess-and-shell.md)
