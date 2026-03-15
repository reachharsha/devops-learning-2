---
title: "Python for DevOps Automation: 32B - Practice Pack (Part 2)"
render_with_liquid: false
---

# Lesson 32B — Practice Pack (Part 2)

This practice pack is designed to make you feel **ready for the mini projects**.

You’ll practice real DevOps patterns:

- CLI arguments
- env var overrides
- running commands
- logging
- regex parsing
- dates/time
- CSV and JSON outputs
- (optional) calling an HTTP API

## Objectives

- Practice combining 3–5 concepts in one script
- Get comfortable with “glue code” automation patterns
- Learn to debug failures using error messages and print/log output

## How to use this pack

- Create a new folder (example): `practice2/`
- Solve one exercise at a time
- After each exercise:
  - run it 2–3 times with different inputs
  - intentionally break it once and fix it

## Exercise 1 — CLI + env var override

Goal:

- read `--env` from CLI (choices: dev/stage/prod)
- if `APP_ENV` env var exists, it overrides the CLI

Create `env_override.py`:

```python
import argparse
import os


def parse_args():
    p = argparse.ArgumentParser()
    p.add_argument("--env", choices=["dev", "stage", "prod"], default="dev")
    return p.parse_args()


def main():
    args = parse_args()

    env = args.env
    env_override = os.getenv("APP_ENV")
    if env_override:
        env = env_override

    print("final env:", env)


if __name__ == "__main__":
    main()
```

Try:

```bash
python3 env_override.py --env stage
APP_ENV=prod python3 env_override.py --env stage
```

Expected output:

```text
final env: stage
final env: prod
```

## Exercise 2 — Run a command safely (`subprocess`)

Goal:

- run `uname -s`
- print stdout
- if command fails, exit non-zero

Create `run_uname.py`:

```python
import subprocess


def main():
    try:
        r = subprocess.run(["uname", "-s"], text=True, capture_output=True, check=True)
    except subprocess.CalledProcessError as e:
        print("ERROR: command failed")
        print("exit:", e.returncode)
        raise SystemExit(1)

    print(r.stdout.strip())


if __name__ == "__main__":
    main()
```

Expected output (example):

```text
Darwin
```

## Exercise 3 — Parse ERROR lines from a log (streaming)

Goal:

- read a file line-by-line
- count lines starting with `ERROR`

Create `sample.log`:

```text
INFO start
ERROR timeout
INFO retry
ERROR failed
```

Create `count_errors.py`:

```python
from pathlib import Path


def main():
    path = Path("sample.log")
    if not path.exists():
        print("ERROR: missing sample.log")
        raise SystemExit(2)

    count = 0
    with path.open("r", encoding="utf-8") as f:
        for line in f:
            if line.startswith("ERROR"):
                count += 1

    print("errors:", count)


if __name__ == "__main__":
    main()
```

Expected output:

```text
errors: 2
```

## Exercise 4 — Extract IP addresses with regex

Goal:

- find all IPs in a text block
- print them uniquely (dedupe)

Create `extract_ips.py`:

```python
import re


def main():
    text = """\
client=10.0.0.1 path=/
client=10.0.0.2 path=/health
client=10.0.0.1 path=/login
"""

    ips = re.findall(r"\b\d+\.\d+\.\d+\.\d+\b", text)
    unique = sorted(set(ips))
    print("unique_ips:", unique)


if __name__ == "__main__":
    main()
```

Expected output:

```text
unique_ips: ['10.0.0.1', '10.0.0.2']
```

## Exercise 5 — Parse time + compute age in seconds

Goal:

- parse an ISO-like UTC timestamp `...Z`
- compute “how many seconds ago” (approx)

Create `age_seconds.py`:

```python
from datetime import datetime, timezone


def main():
    text = "2026-03-15T10:05:30Z"
    dt = datetime.strptime(text, "%Y-%m-%dT%H:%M:%SZ").replace(tzinfo=timezone.utc)

    now = datetime.now(timezone.utc)
    age = (now - dt).total_seconds()

    print("age_seconds:", int(age))


if __name__ == "__main__":
    main()
```

Expected output:

- a non-negative number (it depends on current time)

## Exercise 6 — Read CSV and filter only prod

Goal:

- read a CSV inventory
- print only rows where env=prod

Create `inventory.csv`:

```csv
host,env,ip
web-01,prod,10.0.0.10
api-01,stage,10.0.1.10
web-02,prod,10.0.0.11
```

Create `filter_prod_csv.py`:

```python
import csv


def main():
    with open("inventory.csv", "r", encoding="utf-8", newline="") as f:
        reader = csv.DictReader(f)
        for row in reader:
            if row.get("env") == "prod":
                print(row.get("host"), row.get("ip"))


if __name__ == "__main__":
    main()
```

Expected output:

```text
web-01 10.0.0.10
web-02 10.0.0.11
```

## Exercise 7 (Optional) — HTTP GET with timeout

Goal:

- call a URL
- fail clearly on errors
- print a small piece of info

Install:

```bash
python3 -m pip install requests
```

Create `http_check.py`:

```python
import requests


def main():
    url = "https://httpbin.org/status/200"

    try:
        r = requests.get(url, timeout=5)
        r.raise_for_status()
    except requests.RequestException as e:
        print("HTTP ERROR:", e)
        raise SystemExit(1)

    print("status:", r.status_code)


if __name__ == "__main__":
    main()
```

Expected output:

```text
status: 200
```

## Common Mistakes (With Errors)

### Mistake 1 — Running from the wrong folder

Typical error:

```text
FileNotFoundError: ...
```

Fix: run `pwd` in your terminal and ensure you are in the folder with your files.

### Mistake 2 — Forgetting conversions

Env vars are strings. CLI parsing with `type=int` helps.

### Mistake 3 — Regex dots not escaped

`\.` is a literal dot. A plain `.` matches any character.

## Quick Reference

- CLI: `argparse`
- Env: `os.getenv()`
- Commands: `subprocess.run([...], check=True, capture_output=True, text=True)`
- Logs: `with open(...)` line-by-line
- Regex: `re.findall(r"...", text)`
- Time: `datetime.now(timezone.utc)`
- CSV: `csv.DictReader`
- HTTP: `requests.get(..., timeout=5)`

## Next

Next: [Lesson 33 — Mini Project 1 (Log Analyzer CLI)](33-mini-project-log-analyzer-cli.md)
