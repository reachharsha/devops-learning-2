---
title: "Python for DevOps Automation: 21 - Command-Line Arguments (argparse)"
render_with_liquid: false
---

# Lesson 21 — Command-Line Arguments (`argparse`)

DevOps scripts should be flexible.

Instead of editing the code each time, you pass inputs like:

- `--env prod`
- `--timeout 10`
- `--config config.json`

## Objectives

- Understand what command-line arguments are
- Use `sys.argv` (basic idea)
- Use `argparse` for real scripts
- Provide helpful `--help`
- Validate inputs (choices, types)

## Mental Model

Command-line arguments are like **fill-in-the-blank knobs** for your script.

- Your script defines the knobs.
- The user sets the knobs at run time.

## `sys.argv` (what it is)

Python stores raw CLI arguments in a list named `sys.argv`.

```python
import sys
print(sys.argv)
```

But for real scripts, parsing by hand becomes messy.

## `argparse` (recommended)

Create `check_threshold.py`:

```python
import argparse


def parse_args():
    p = argparse.ArgumentParser(description="Simple threshold checker")
    p.add_argument("--value", type=int, required=True, help="Measured value")
    p.add_argument("--threshold", type=int, default=80, help="Alert threshold")
    p.add_argument(
        "--mode",
        choices=["ge", "gt"],
        default="ge",
        help="Comparison: ge (>=) or gt (>)",
    )
    return p.parse_args()


def main():
    args = parse_args()

    if args.mode == "ge":
        breached = args.value >= args.threshold
    else:
        breached = args.value > args.threshold

    if breached:
        print("ALERT")
    else:
        print("OK")


if __name__ == "__main__":
    main()
```

Run:

```bash
python3 check_threshold.py --value 91 --threshold 90
```

Expected output:

```text
ALERT
```

Try help:

```bash
python3 check_threshold.py --help
```

## Common Mistakes (With Errors)

### Mistake 1 — Missing required argument

If you forget `--value`:

```text
error: the following arguments are required: --value
```

Fix: provide required args or make them optional with defaults.

### Mistake 2 — Type conversion errors

If you pass a non-integer to `type=int`:

```text
error: argument --value: invalid int value: 'abc'
```

Fix: pass correct types; `argparse` is helping you early.

## Quick Reference

- Create parser: `argparse.ArgumentParser(...)`
- Add arg: `add_argument("--name", type=int, required=True)`
- Choices: `choices=["a", "b"]`
- Parse: `args = parser.parse_args()`
- Help: `--help`

## Next

Next: [Lesson 22 — OS, Sys, Env Vars, Exit Codes](22-os-sys-env-exit-codes.md)
