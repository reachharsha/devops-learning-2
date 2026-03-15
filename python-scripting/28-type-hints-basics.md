---
title: "Python Scripting: 28 - Type Hints (Basics)"
render_with_liquid: false
---

# Lesson 28 — Type Hints (Basics)

## Objectives

- Understand what type hints are
- Annotate functions
- Know what type hints do (and don’t do)

## Concepts

Type hints help editors and tools catch mistakes earlier.

They do **not** change how Python runs by default.

## Hands-on Lab

Create `typing_demo.py`:

```python
from typing import List


def total(values: List[int]) -> int:
    return sum(values)


print(total([1, 2, 3]))
```

## Quick Check

1) Do type hints enforce types at runtime automatically?
2) Why are type hints useful in larger scripts?

## Next

[Lesson 29: dataclasses](29-dataclasses.md)
