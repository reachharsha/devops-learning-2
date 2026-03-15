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
- Use indexing and slicing on lists
- Avoid common mutability surprises

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
- `extend(list)` add many items
- `pop()` remove and return last item
- `remove(x)` remove first matching value
- `sorted(list)` returns a new sorted list
- `len(list)` number of items
- `in` membership test: `"web-01" in servers`

### Indexing and slicing (lists)

Lists are ordered, so you can access items by position.

```python
servers = ["web-01", "web-02", "api-01"]
print(servers[0])   # first item
print(servers[-1])  # last item
```

Slicing returns a new list:

```python
print(servers[0:2])  # first two items
```

Rule: `list[start:end]` includes `start` but excludes `end`.

## Tuples

Tuples look like lists but use parentheses and are typically used for fixed “records”.

```python
host = ("web-01", "10.0.0.10", "prod")
name, ip, env = host
print(name, ip, env)
```

Tuples are immutable. You can’t do `host[0] = "x"`.

## Sets (uniques)

```python
ips = ["10.0.0.1", "10.0.0.2", "10.0.0.1"]
unique_ips = set(ips)
print(unique_ips)
```

Note: sets are not ordered, so printing may show items in any order.

### Set operations (useful for comparisons)

```python
a = {"web-01", "web-02"}
b = {"web-02", "api-01"}

print(a | b)  # union
print(a & b)  # intersection
print(a - b)  # difference
```

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

## Hands-on Lab 2 — Filter only prod servers (list + if)

Create `filter_prod.py`:

```python
inventory = [
    "prod-web-01",
    "prod-web-02",
    "stage-api-01",
    "dev-worker-01",
]

prod = []
for host in inventory:
    if host.startswith("prod-"):
        prod.append(host)

print("prod:", prod)
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

### Mistake 3 — Two variables pointing to the same list

Bad:

```python
targets = ["web-01"]
other = targets
other.append("web-02")
print(targets)
```

Both names refer to the same list (mutable object).

Fix: make a copy if you need a separate list:

```python
other = targets.copy()
```

## Quick Reference

- List literal: `[]`
- Tuple literal: `()`
- Set from list: `set(list)`
- Add to list: `list.append(x)`
- Count items: `len(x)`
- Membership: `x in collection`
- Copy list: `new = old.copy()`
- Sort (new list): `sorted(list)`

## Next

Next: [Lesson 16 — Dictionaries (key/value)](16-dictionaries.md)

