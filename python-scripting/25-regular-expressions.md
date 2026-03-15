---
title: "Python for DevOps Automation: 25 - Regular Expressions (re)"
render_with_liquid: false
---

# Lesson 25 — Regular Expressions (`re`)

Regex (regular expressions) are a powerful way to match patterns in text.

DevOps uses:

- extracting IPs
- pulling request IDs
- parsing structured-ish logs

## Objectives

- Understand what regex is (pattern matching)
- Use `re.search` and `re.findall`
- Use capturing groups
- Use raw strings `r"..."`
- Avoid common regex pitfalls

## Mental Model

Regex is like a **metal detector** for text.

- You sweep a pattern over a line
- It beeps where it matches

## Start simple: find an IP address

Create `find_ip.py`:

```python
import re

text = "client=10.1.2.3 status=200"

m = re.search(r"\b\d+\.\d+\.\d+\.\d+\b", text)
if m:
    print("ip:", m.group(0))
else:
    print("no ip")
```

Expected output:

```text
ip: 10.1.2.3
```

Explain the pattern:

- `\d+` one-or-more digits
- `\.` a literal dot (dot is special in regex)
- `\b` word boundary (helps avoid partial matches)

## Capturing groups

Create `parse_kv_regex.py`:

```python
import re

line = "level=ERROR service=api msg=timeout"

pairs = re.findall(r"(\w+)=([^\s]+)", line)
print(pairs)

data = {k: v for k, v in pairs}
print("service:", data.get("service"))
```

Expected output:

```text
[('level', 'ERROR'), ('service', 'api'), ('msg', 'timeout')]
service: api
```

## Common Mistakes (With Errors)

### Mistake 1 — Forgetting raw strings

Bad:

```python
"\d+"  # this is ok, but gets harder with more backslashes
```

Beginner rule: use raw strings for regex:

```python
r"\d+"
```

### Mistake 2 — `.` matches anything

If you write `10.1.2.3` as `10.1.2.3` in regex, the dots match any character.

Fix: escape dots: `\.`

## Quick Reference

- Search first match: `re.search(pattern, text)`
- All matches: `re.findall(pattern, text)`
- Match text: `m.group(0)`
- Groups: `( ... )`
- Raw: `r"..."`

## Next

Next: [Lesson 26 — Dates & Time (datetime)](26-dates-and-time-datetime.md)
