---
title: "Python for DevOps Automation: 33 - Mini Project 1 (Log Analyzer CLI)"
render_with_liquid: false
---

# Lesson 33 — Mini Project 1: Log Analyzer CLI

Now you’ll combine skills:

- argparse
- pathlib
- string parsing / regex
- JSON report output
- exit codes

## Objectives

Build a CLI tool that:

- reads a log file
- counts ERROR lines
- writes a JSON report
- exits non-zero if errors exceed a threshold

## Project: `log_analyze.py`

Create `log_analyze.py`:

```python
import argparse
import json
from pathlib import Path


def parse_args():
    p = argparse.ArgumentParser(description="Analyze a log file and count errors")
    p.add_argument("--log", required=True, help="Path to log file")
    p.add_argument("--threshold", type=int, default=1, help="Max allowed ERROR lines")
    p.add_argument("--out", default="report.json", help="Output report path")
    return p.parse_args()


def count_errors(path: Path) -> int:
    count = 0
    with path.open("r", encoding="utf-8") as f:
        for line in f:
            if line.startswith("ERROR"):
                count += 1
    return count


def main():
    args = parse_args()
    log_path = Path(args.log)

    if not log_path.exists():
        print("ERROR: log file not found:", log_path)
        raise SystemExit(2)

    errors = count_errors(log_path)

    report = {
        "log": str(log_path),
        "errors": errors,
        "threshold": args.threshold,
        "ok": errors <= args.threshold,
    }

    Path(args.out).write_text(json.dumps(report, indent=2) + "\n", encoding="utf-8")
    print("wrote:", args.out)

    if errors > args.threshold:
        raise SystemExit(1)


if __name__ == "__main__":
    main()
```

## Try it

Create `sample.log`:

```text
INFO started
ERROR timeout
ERROR retry failed
INFO done
```

Run:

```bash
python3 log_analyze.py --log sample.log --threshold 1 --out report.json
```

Expected output:

```text
wrote: report.json
```

The exit code should be non-zero because errors=2 > threshold=1.

## Common Mistakes

- Forgetting `--log` (argparse will error)
- Not using `encoding="utf-8"` (possible decode issues)
- Not writing a newline at end of JSON (minor, but nice)

## Extension Checklist (make it more “real”)

Try these one-by-one (don’t do all at once):

- Add `--prefix` (default `ERROR`) so you can count `WARN` too
- Make counting case-insensitive (`error`, `Error`, `ERROR`)
- Add total line count and include it in the JSON report
- Add `--fail-code` (default `1`) so CI can distinguish failures
- Add logging (`logging` module) and a `--debug` flag
- Handle decode errors explicitly (`errors="replace"`), and include a warning count
- Write a small unit test for `count_errors()` (use `unittest`)

## Quick Reference

- Argparse required: `add_argument("--x", required=True)`
- Safe open: `with Path(...).open(...) as f:`
- Exit failure: `raise SystemExit(1)`

## Next

Next: [Lesson 34 — Mini Project 2 (Config-driven checks)](34-mini-project-config-driven-checks.md)
