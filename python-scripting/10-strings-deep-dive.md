---
title: "Python for DevOps Automation: 10 - Strings Deep Dive (DevOps)"
render_with_liquid: false
---

# Lesson 10 — Strings Deep Dive (DevOps)

## Objectives

By the end, you can:

- Explain what a string is and why strings are immutable
- Use f-strings for readable output
- Use indexing and slicing (`s[0]`, `s[1:4]`)
- Use core string methods (`strip`, `split`, `join`, `replace`, `startswith`)
- Parse typical DevOps text (URLs, log lines)

## What is a string?

A string (`str`) is text.

In DevOps work, almost everything starts as a string:

- command output
- logs
- file contents
- URLs
- environment variables

## Strings are immutable

Immutable means: you can’t change the existing string object.

Operations create a new string:

```python
s = "error"
t = s.replace("error", "ok")
print(s)
print(t)
```

## Indexing (one character)

```python
host = "web-01"
print(host[0])   # 'w'
print(host[-1])  # '1'
```

## Slicing (a range)

```python
host = "web-01"
print(host[0:3])  # 'web'
```

Rule: `s[start:end]` includes `start` but excludes `end`.

## Core methods you’ll use constantly

- `strip()` remove surrounding whitespace/newlines
- `split("/")` split into pieces
- `"-".join(parts)` join pieces
- `replace(old, new)`
- `startswith(prefix)` / `endswith(suffix)`
- `splitlines()` for multi-line text

## Escape sequences (special characters)

Some characters are written with backslashes:

- `\n` newline
- `\t` tab

Example:

```python
print("line1\nline2")
```

## Raw strings (useful for regex and Windows paths)

If you see a lot of backslashes, raw strings reduce escaping:

```python
pattern = r"\d+"  # \d means digit in regex
```

## `in` checks (very common in log parsing)

```python
line = "ERROR timeout"
if "ERROR" in line:
    print("found error")
```

## Hands-on Lab 2 — Parse a key=value log line

DevOps logs often contain fields like `key=value`.

Create `parse_kv_log.py`:

```python
line = "ts=2026-03-15 level=ERROR service=api msg=timeout"

parts = line.split()
fields = {}

for part in parts:
    if "=" not in part:
        continue
    key, value = part.split("=", 1)
    fields[key] = value

print("service:", fields.get("service"))
print("level:", fields.get("level"))
print("msg:", fields.get("msg"))
```

Expected output:

```text
service: api
level: ERROR
msg: timeout
```

## Hands-on Lab

Create `parse_url.py`:

```python
url = "https://api.example.com/v1/health"

if url.startswith("https://"):
    without_scheme = url[len("https://"):]
else:
    without_scheme = url

host = without_scheme.split("/")[0]

print(f"url={url}")
print(f"host={host}")
```

Expected output:

```text
url=https://api.example.com/v1/health
host=api.example.com
```

## Common mistakes

### Mistake 1 — IndexError from bad splitting

If you access a split part that doesn’t exist, you get `IndexError`.

Fix: check `startswith()` first or handle both cases.

### Mistake 2 — Forgetting that `replace()` returns a new string

Bad:

```python
s = "error"
s.replace("error", "ok")
print(s)
```

Output is still `error` because you didn’t store the new string.

Fix:

```python
s = s.replace("error", "ok")
```

### Mistake 3 — Indexing past the end

Bad:

```python
s = "web"
print(s[10])
```

Typical error:

```text
IndexError: string index out of range
```

Fix: check `len(s)` or use safe parsing (split/startswith) instead of fixed indexes.

## DevOps use case

Logs, command output, URLs, configs all start as strings.

## Quick Reference

- f-string: `f"{name} {value:.2f}"`
- Methods: `strip split join replace startswith endswith`
- Indexing: `s[0]`, last char `s[-1]`
- Slicing: `s[a:b]` includes a, excludes b
- Special chars: `\n`, `\t`

## Next

[Lesson 11: Practice Pack (Part 1)](11-practice-pack-part1.md)
