---
title: "Python for DevOps Automation: 11 - Practice Pack (Part 1)"
render_with_liquid: false
---

# Lesson 11 — Practice Pack (Part 1)

Run these small scripts to build confidence.

## Exercise 1 — Variable swap (server roles)

Create `swap_roles.py`:

```python
primary = "web-01"
secondary = "web-02"

print("before:", primary, secondary)
primary, secondary = secondary, primary
print("after:", primary, secondary)
```

Expected output:

```text
before: web-01 web-02
after: web-02 web-01
```

## Exercise 2 — Deployment metadata

Create `deploy_info.py`:

```python
app = input("App name: ")
env = input("Environment (dev/stage/prod): ")
version = input("Version: ")

print(f"Deploying app={app} env={env} version={version}")
```

## Exercise 3 — Extract hostname from URL

Create `extract_host.py`:

```python
url = input("Enter URL: ").strip()

if url.startswith("https://"):
    url = url[len("https://"):]
elif url.startswith("http://"):
    url = url[len("http://"):]

host = url.split("/")[0]
print("host:", host)
```

## Exercise 4 — Simple calculator with safe input

Create `calc.py`:

```python
a_text = input("a: ")
b_text = input("b: ")

try:
    a = float(a_text)
    b = float(b_text)
except ValueError:
    print("ERROR: numbers only")
    raise SystemExit(1)

print("sum:", a + b)
print("diff:", a - b)
print("mul:", a * b)

if b == 0:
    print("div: ERROR (division by zero)")
else:
    print("div:", a / b)
```

## Exercise 5 — Bytes to human readable

Create `bytes_human.py`:

```python
bytes_text = input("Bytes: ")

try:
    n = int(bytes_text)
except ValueError:
    print("ERROR: enter an integer")
    raise SystemExit(1)

units = ["B", "KB", "MB", "GB", "TB"]
size = float(n)
unit_index = 0

while size >= 1024 and unit_index < len(units) - 1:
    size /= 1024
    unit_index += 1

print(f"{n} bytes = {size:.2f} {units[unit_index]}")
```

## Quick Reference

- Validate inputs early
- Prefer venv per project
- Use f-strings

## Next

Next: [Lesson 12 — Conditionals](12-conditionals.html)

