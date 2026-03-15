---
title: "Python Scripting: 10 - Collections (list/dict/set/tuple)"
render_with_liquid: false
---

# Lesson 10 — Collections (list/dict/set/tuple)

## Objectives

- Use lists for ordered items
- Use dicts for key/value data
- Understand tuples and sets

## Concepts

### List

```python
names = ["a", "b", "c"]
```

### Dict

```python
user = {"name": "Alice", "age": 30}
```

### Tuple

Tuples are like lists but typically treated as “fixed”:

```python
point = (10, 20)
```

### Set

Sets store unique items:

```python
unique = {"a", "a", "b"}
```

## Hands-on Lab

Create `collections_demo.py`:

```python
fruits = ["apple", "banana", "mango"]
fruits.append("orange")
print(fruits)

config = {"host": "localhost", "port": 8080}
print(config["host"], config["port"])

tags = {"devops", "python", "python"}
print(tags)
```

## Quick Check

1) Which type is best for key/value data?
2) Which type removes duplicates automatically?

## Next

[Lesson 11: Modules & Imports](11-modules-and-imports.md)
