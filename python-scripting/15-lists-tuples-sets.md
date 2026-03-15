---
title: "Python for DevOps Automation: 15 - Lists, Tuples, Sets"
render_with_liquid: false
---

# Lesson 15 — Lists, Tuples, Sets

These are the simplest “containers” for multiple values.

In DevOps automation, you’ll store things like:

- a list of servers
- a list of paths to check
- unique usernames / IPs you saw in logs

## Objectives

- Understand when to use a `list`, `tuple`, or `set`
- Add/remove items from a list
- Deduplicate values with a set

## Mental Model

- `list` = a clipboard list you can edit
- `tuple` = a sealed package (fixed)
- `set` = a bag of unique items (no duplicates)

## Lists

```python
servers = ["web-01", "web-02"]
servers.append("api-01")
print(servers)
```

Expected output:

```text
['web-01', 'web-02', 'api-01']
```

Common operations:

- `append(x)` add to end
- `len(list)` number of items
- `in` membership test: `"web-01" in servers`

## Tuples

Tuples look like lists but use parentheses and are typically used for fixed “records”.

```python
host = ("web-01", "10.0.0.10", "prod")
name, ip, env = host
print(name, ip, env)
```

## Sets (uniques)

```python
ips = ["10.0.0.1", "10.0.0.2", "10.0.0.1"]
unique_ips = set(ips)
print(unique_ips)
```

Note: sets are not ordered, so printing may show items in any order.

## Hands-on Lab — Dedupe hosts from “inventory” text

Create `dedupe_hosts.py`:

```python
inventory = """\
web-01
web-02
web-01
api-01
api-01
"""

hosts = []
for line in inventory.splitlines():
    line = line.strip()
    if not line:
        continue
    hosts.append(line)

print("all:", hosts)
print("count:", len(hosts))

unique_hosts = sorted(set(hosts))
print("unique:", unique_hosts)
print("unique_count:", len(unique_hosts))
```

Expected output:

```text
all: ['web-01', 'web-02', 'web-01', 'api-01', 'api-01']
count: 5
unique: ['api-01', 'web-01', 'web-02']
unique_count: 3
```

## Common Mistakes

### Mistake 1 — Using a set when order matters

If you need stable order, keep a list and dedupe later with `sorted(set(...))`.

### Mistake 2 — IndexError

Bad:

```python
servers = ["web-01"]
print(servers[1])
```

Typical error:

```text
IndexError: list index out of range
```

Fix: check length (`len(...)`) or iterate with `for`.

## Quick Reference

- List literal: `[]`
- Tuple literal: `()`
- Set from list: `set(list)`
- Add to list: `list.append(x)`
- Count items: `len(x)`
- Membership: `x in collection`

## Next

Next: [Lesson 16 — Dictionaries (key/value)](16-dictionaries.html)

