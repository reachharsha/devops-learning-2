---
title: "Python Scripting: 23 - CLI Subcommands"
render_with_liquid: false
---

# Lesson 23 — CLI Subcommands

## Objectives

- Build CLIs like `git status` / `git log`
- Use subcommands with `argparse`
- Structure a script for growth

## Concepts

Subcommands let you create one tool with multiple actions.

## Hands-on Lab

Create `tool.py`:

```python
import argparse


def cmd_hello(args):
    print(f"Hello, {args.name}!")


def cmd_add(args):
    print(args.a + args.b)


def main():
    parser = argparse.ArgumentParser(prog="tool")
    sub = parser.add_subparsers(dest="command", required=True)

    p_hello = sub.add_parser("hello", help="Greet someone")
    p_hello.add_argument("name")
    p_hello.set_defaults(func=cmd_hello)

    p_add = sub.add_parser("add", help="Add two numbers")
    p_add.add_argument("a", type=int)
    p_add.add_argument("b", type=int)
    p_add.set_defaults(func=cmd_add)

    args = parser.parse_args()
    args.func(args)


if __name__ == "__main__":
    main()
```

Run:

```bash
python3 tool.py --help
python3 tool.py hello Alice
python3 tool.py add 10 20
```

## Quick Check

1) What are subcommands?
2) Why do they help your automation scripts scale?

## Next

[Lesson 24: Config & Env Vars](24-config-and-env-vars.md)
