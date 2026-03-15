---
title: "Python for DevOps Automation: 18 - JSON & YAML Config (read/validate)"
render_with_liquid: false
---

# Lesson 18 — JSON & YAML Config (read/validate)

Most automation scripts need **configuration**:

- which environment (dev/stage/prod)
- which region
- which services/hosts
- thresholds (CPU, disk)

JSON and YAML are the two most common formats you’ll meet.

## Objectives

- Read JSON config using the built-in `json` module
- (Optional) Read YAML using `PyYAML`
- Validate required keys and types (basic “schema” checks)
- Merge config + environment variables safely
- Write JSON back to disk (reports)
- Understand common JSON/YAML gotchas for beginners

## Mental Model

Config is like a **control panel**:

- Your script is the machine.
- Config are the knobs.

Hard-coding knobs inside the script makes it brittle.

## JSON basics

JSON is strict:

- keys and strings use **double quotes**
- no comments

Example `config.json`:

```json
{
  "app": "payments",
  "env": "prod",
  "retries": 3,
  "timeout_seconds": 5,
  "targets": ["web-01", "web-02"]
}
```

### Read JSON with Python

Create `read_json_config.py`:

```python
from pathlib import Path
import json


def load_json(path):
    text = Path(path).read_text(encoding="utf-8")
    return json.loads(text)


config = load_json("config.json")
print("env:", config.get("env"))
print("retries:", config.get("retries"))
print("targets:", config.get("targets"))
```

## Writing JSON (for reports)

Automation often produces machine-readable output.

Create `write_report_json.py`:

```python
from pathlib import Path
import json

report = {
    "service": "api",
    "healthy": True,
    "errors": 2,
}

Path("report.json").write_text(
    json.dumps(report, indent=2, sort_keys=True) + "\n",
    encoding="utf-8",
)

print("wrote report.json")
```

## Basic validation (required keys + types)

Automation fails most often when config is missing or wrong type.

Create `validate_config.py`:

```python
from pathlib import Path
import json


def load_json(path):
    return json.loads(Path(path).read_text(encoding="utf-8"))


def require_key(d, key, expected_type):
    if key not in d:
        raise KeyError(f"Missing required key: {key}")
    value = d[key]
    if not isinstance(value, expected_type):
        raise TypeError(f"Key '{key}' must be {expected_type.__name__}, got {type(value).__name__}")
    return value


try:
    cfg = load_json("config.json")
    require_key(cfg, "env", str)
    require_key(cfg, "retries", int)
    require_key(cfg, "targets", list)
except (OSError, json.JSONDecodeError, KeyError, TypeError) as e:
    print("CONFIG ERROR:", e)
    raise SystemExit(1)

print("config OK")
```

## YAML (optional but common in DevOps)

YAML is common (Kubernetes manifests, CI pipelines), but Python needs a library.

Install in your venv:

```bash
python3 -m pip install pyyaml
```

Example `config.yaml`:

```yaml
app: payments
env: prod
retries: 3
targets:
  - web-01
  - web-02
```

Create `read_yaml_config.py`:

```python
from pathlib import Path

try:
    import yaml
except ImportError:
    print("ERROR: PyYAML not installed. Run: python3 -m pip install pyyaml")
    raise SystemExit(1)


cfg = yaml.safe_load(Path("config.yaml").read_text(encoding="utf-8"))
print(cfg)
```

We use `safe_load` to avoid unsafe YAML features.

### YAML gotcha: types can be implicit

YAML may interpret values as numbers/booleans automatically.

Example:

```yaml
retries: 3
healthy: true
```

In JSON, everything is explicit.

## Hands-on Lab — Config + env var overrides

Goal: allow config file defaults, but let environment variables override.

Create `config_with_env.py`:

```python
import os
import json
from pathlib import Path


cfg = json.loads(Path("config.json").read_text(encoding="utf-8"))

# override if env var exists
env_override = os.getenv("APP_ENV")
if env_override:
    cfg["env"] = env_override

timeout_override = os.getenv("TIMEOUT_SECONDS")
if timeout_override:
    try:
        cfg["timeout_seconds"] = int(timeout_override)
    except ValueError:
        print("CONFIG ERROR: TIMEOUT_SECONDS must be an integer")
        raise SystemExit(1)

print("final config:")
print(cfg)
```

Example run:

```bash
APP_ENV=stage TIMEOUT_SECONDS=10 python3 config_with_env.py
```

## Common Mistakes (With Errors)

### Mistake 1 — JSON trailing commas

Bad JSON:

```json
{"retries": 3,}
```

Typical error:

```text
json.decoder.JSONDecodeError: Expecting property name enclosed in double quotes
```

### Mistake 2 — YAML tabs

YAML indentation must use spaces (tabs often break parsing).

### Mistake 3 — YAML indentation levels

This is wrong:

```yaml
targets:
- web-01
    - web-02
```

Indentation must be consistent.

### Mistake 4 — Wrong types from env vars

Environment variables are always strings.

Convert and validate (e.g., `int(timeout_override)`) and handle `ValueError`.

## Quick Reference

- JSON: `import json` → `json.loads(text)`
- YAML: `pip install pyyaml` → `yaml.safe_load(text)`
- Validate required keys and types early
- Env vars are strings → convert + validate

## Next

Next: [Lesson 19 — Exceptions & Error Handling](19-exceptions-error-handling.md)
