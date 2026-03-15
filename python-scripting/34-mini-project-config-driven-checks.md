---
title: "Python for DevOps Automation: 34 - Mini Project 2 (Config-driven checks)"
render_with_liquid: false
---

# Lesson 34 — Mini Project 2: Config-driven Checks

In real automation, you don’t hardcode targets.

You read config (JSON/YAML) and perform checks.

## Objective

Build a script that:

- reads a JSON config of services
- performs a simple “check” per service (simulated)
- logs results
- writes a report

## Example config

Create `services.json`:

```json
{
  "services": [
    {"name": "api", "timeout_seconds": 2},
    {"name": "worker", "timeout_seconds": 2}
  ]
}
```

## Script: `run_checks.py`

```python
import json
import logging
from pathlib import Path


logging.basicConfig(level=logging.INFO, format="%(levelname)s %(message)s")
log = logging.getLogger("checks")


def load_config(path: str) -> dict:
    return json.loads(Path(path).read_text(encoding="utf-8"))


def check_service(service: dict) -> dict:
    # Simulated check: mark api healthy, worker unhealthy
    name = service.get("name")
    healthy = name == "api"
    return {"name": name, "healthy": healthy}


def main():
    cfg = load_config("services.json")
    services = cfg.get("services", [])

    results = []
    for s in services:
        r = check_service(s)
        results.append(r)
        log.info("service=%s healthy=%s", r["name"], r["healthy"])

    report = {"results": results}
    Path("checks-report.json").write_text(json.dumps(report, indent=2) + "\n", encoding="utf-8")
    print("wrote checks-report.json")


if __name__ == "__main__":
    main()
```

Expected output:

```text
INFO service=api healthy=True
INFO service=worker healthy=False
wrote checks-report.json
```

## Common Mistakes

- Assuming keys exist (use `.get()` for optional values)
- Printing secrets from config/env vars
- Not validating config structure early

## Quick Reference

- Load JSON: `json.loads(Path(...).read_text())`
- Logging: `logging.basicConfig(...)`
- Report: `Path("x").write_text(json.dumps(...))`

## Next

Next: [Lesson 35 — Capstone Checklist + Next Steps](35-capstone-next-steps.md)
