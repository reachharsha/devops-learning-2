---
title: "Python for DevOps Automation: 07 - Variables & Data Types"
render_with_liquid: false
---

# Lesson 07 — Variables & Data Types

## Objectives

By the end, you can:

- Explain what a variable is (in Python)
- Create variables and re-assign them safely
- Recognize the common built-in types used in automation (`str`, `int`, `float`, `bool`, `NoneType`)
- Use `type()` to check what you have
- Understand **mutable** vs **immutable** objects (and why that matters in scripts)

## Real-world analogy

### Variable = label pointing to a value

When you write:

```text
hostname  ->  "web-01"
```

That arrow is important: in Python, a variable name is like a **label** that points to a value.

`=` means **assign** (attach the label to a value), not “math equals”.

## Big Picture: How Python stores values

Python creates objects (values) in memory. Variables point to those objects.

```
name (label) ---> [object in memory]
```

This is why you can do:

```python
hostname = "web-01"
hostname = "web-02"  # label points to a different value now
```

You didn’t “edit” the old string — you re-assigned the label.

## Variables (the basics)

### 1) Defining a variable

You define a variable by assigning a value:

```python
service = "api"
retries = 3
timeout_seconds = 5
```

The left side is the variable name. The right side is the value.

### 2) Re-assigning a variable

Re-assignment is normal:

```python
retries = 3
retries = retries + 1
print(retries)  # 4
```

### 3) Naming rules (must know)

Valid names:

- can contain letters, digits, underscore
- cannot start with a digit
- case-sensitive (`Env` and `env` are different)

Good (clear) names for DevOps scripts:

```python
disk_usage_percent = 87
is_prod = True
log_path = "/var/log/syslog"
```

Avoid:

- `x`, `tmp`, `a1` (too vague)
- using Python keywords like `for`, `if`, `class`

## Data Types (what kind of value is it?)

A “type” is the category of a value.

For example:

- a hostname is text → `str`
- a retry count is a whole number → `int`
- a CPU load average is often decimal → `float`

Python is **dynamically typed**:

- You don’t write types explicitly when creating variables.
- The value itself has a type.

### Core types you’ll use constantly

#### `str` (string) — text

```python
hostname = "web-01"
```

Strings are used for paths, commands, URLs, log lines.

#### `int` — whole numbers

```python
retries = 3
port = 443
```

#### `float` — decimals

```python
cpu_load = 0.75
```

#### `bool` — True/False

```python
service_up = True
has_errors = False
```

#### `None` — “no value / unknown / missing”

```python
last_error = None
```

`None` is not an empty string and not zero. It means “nothing here”.

### Check a value’s type with `type()`

```python
value = "web-01"
print(type(value))
```

Typical output:

```text
<class 'str'>
```

## Converting between types (very common)

Most DevOps scripts read text from:

- `input()`
- environment variables
- files
- CLI tools

That text often needs conversion:

```python
retries_text = "3"
retries = int(retries_text)
```

If conversion fails, you get a `ValueError`.

## Mutability (mutable vs immutable)

This is a key beginner concept.

### Definition

- **Mutable** object: can be changed *in place* (same object, new content)
- **Immutable** object: cannot be changed in place (changes create a new object)

### Common mutable types

- `list` (e.g., `["web-01", "web-02"]`)
- `dict` (e.g., `{ "env": "prod" }`)
- `set` (e.g., `{ "10.0.0.1", "10.0.0.2" }`)

### Common immutable types

- `str`, `int`, `float`, `bool`
- `tuple`

### Why DevOps engineers should care

Mutability can create surprising bugs when two variables refer to the **same** list/dict.

Example:

```python
targets = ["web-01", "web-02"]
copy_ref = targets

copy_ref.append("api-01")
print(targets)
```

You might expect only `copy_ref` changed, but both names point to the same list.

## Hands-on Labs

### Lab 1 — Variables and types (DevOps-flavored)

Create `types_devops.py`:

```python
hostname = "web-01"          # str
retry_count = 3              # int
cpu_load = 0.75              # float
service_up = True            # bool
last_error = None            # NoneType

print("hostname:", hostname, type(hostname))
print("retry_count:", retry_count, type(retry_count))
print("cpu_load:", cpu_load, type(cpu_load))
print("service_up:", service_up, type(service_up))
print("last_error:", last_error, type(last_error))
```

Expected output shape (types may display the same):

```text
hostname: web-01 <class 'str'>
retry_count: 3 <class 'int'>
cpu_load: 0.75 <class 'float'>
service_up: True <class 'bool'>
last_error: None <class 'NoneType'>
```

### Lab 2 — Converting user input (string → int)

Create `retries_input.py`:

```python
text = input("Retries (e.g., 3): ").strip()

try:
	retries = int(text)
except ValueError:
	print("ERROR: retries must be a whole number")
	raise SystemExit(1)

print("retries is", retries, "type=", type(retries))
```

### Lab 3 — Mutability surprise (two names, one list)

Create `mutable_surprise.py`:

```python
targets = ["web-01", "web-02"]
also_targets = targets

print("before targets:", targets)
print("before also_targets:", also_targets)

also_targets.append("api-01")

print("after targets:", targets)
print("after also_targets:", also_targets)
```

Expected output:

```text
before targets: ['web-01', 'web-02']
before also_targets: ['web-01', 'web-02']
after targets: ['web-01', 'web-02', 'api-01']
after also_targets: ['web-01', 'web-02', 'api-01']
```

This proves the list was changed in place.

## Common mistakes (with real errors)

### Mistake 1 — Using a Python keyword as a variable name

Bad:

```python
class = "api"  # invalid
```

Typical error:

```text
SyntaxError: invalid syntax
```

### Mistake 2 — Using a variable before defining it

Bad:

```python
print(region)
region = "us-east-1"
```

Typical error:

```text
NameError: name 'region' is not defined
```

### Mistake 3 — Doing math on strings

Bad:

```python
retries = "3"
print(retries + 1)
```

Typical error:

```text
TypeError: can only concatenate str (not "int") to str
```

Fix: `int(retries)`.

## DevOps use case

Variables hold:

- config values (timeouts, retries, regions)
- parsed log fields (service, level, message)
- API response data (JSON → dict)

Types matter because automation is strict: a retry count must be a number, not text.

Mutability matters because you often pass lists/dicts between functions.

## Quick Reference

- Assign: `name = value`
- Check type: `type(x)`
- Convert: `int(text)`, `float(text)`, `str(x)`
- Core types: `str`, `int`, `float`, `bool`, `None`
- Mutable: `list`, `dict`, `set`
- Immutable: `str`, `int`, `float`, `bool`, `tuple`

## Next

[Lesson 08: Output, Input, Comments](08-output-input-comments.md)

## Concepts

### Types

- `str` text
- `int` whole numbers
- `float` decimal
- `bool` True/False
- `None` missing value

### Mutability

- Mutable: list/dict/set
- Immutable: str/int/float/tuple

## Hands-on Lab

Create `types_devops.py`:

```python
hostname = "web-01"
retry_count = 3
cpu_load = 0.75
service_up = True
last_error = None

print("hostname:", hostname, type(hostname))
print("retry_count:", retry_count, type(retry_count))
print("cpu_load:", cpu_load, type(cpu_load))
print("service_up:", service_up, type(service_up))
print("last_error:", last_error, type(last_error))

print("id(hostname):", id(hostname))
```

## Common mistakes

- Using reserved keywords as variable names (SyntaxError)

## DevOps use case

Variables hold config values, parsed log fields, and API response data.

## Quick Reference

- Assign: `name = value`
- Types: `str int float bool None`
- Check: `type(x)`
- Mutable: list/dict/set

## Next

[Lesson 08: Output, Input, Comments](08-output-input-comments.md)
