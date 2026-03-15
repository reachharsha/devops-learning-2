---
title: "Python for DevOps Automation: 35 - Capstone + Next Steps"
render_with_liquid: false
---

# Lesson 35 — Capstone Checklist + Next Steps

You now have a complete beginner-to-automation toolkit.

This final lesson is a **capstone checklist** you can follow for any script.

## Capstone checklist (use this every time)

- Inputs
  - Use `argparse` for CLI arguments
  - Use config files (JSON/YAML) for defaults
  - Use env vars for secrets
- Validation
  - validate required keys
  - convert strings → int/bool safely
  - fail early with clear messages
- Reliability
  - timeouts on network calls
  - retries with backoff for transient errors
  - safe writes (temp + replace)
- Observability
  - use `logging` not random prints
  - include enough context in logs (service, host, env)
- Output
  - write machine-readable reports (JSON/CSV)
  - exit non-zero on failure
- Structure
  - split code into modules
  - keep functions small
  - add a few unit tests for core logic

## A small “template” you can reuse

```python
import argparse
import logging


def parse_args():
    p = argparse.ArgumentParser()
    p.add_argument("--config", default="config.json")
    return p.parse_args()


def main():
    logging.basicConfig(level=logging.INFO, format="%(levelname)s %(message)s")
    log = logging.getLogger("tool")
    args = parse_args()
    log.info("starting config=%s", args.config)
    # load config, validate, do work...


if __name__ == "__main__":
    main()
```

## Where to go next

- Learn `pytest` (popular test framework)
- Learn `click` or `typer` (nice CLIs)
- Learn `boto3` for AWS automation
- Learn `paramiko` for SSH automation (careful with keys)
- Learn `asyncio` for high-scale network checks

## Next

Next: return to the course list: [Course Index](../index.html)
