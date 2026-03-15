---
title: "Python for DevOps Automation: 31 - Testing (unittest)"
render_with_liquid: false
---

# Lesson 31 — Testing (`unittest`)

Testing makes automation safer.

Even simple scripts benefit from tests for core logic.

## Objectives

- Understand what a unit test is
- Write a basic `unittest` test
- Run tests from the command line
- Avoid common beginner test issues

## Mental Model

A test is like a **smoke alarm check**.

- You don’t wait for a real fire.
- You verify your alarm works.

## Hands-on Lab — Test a threshold function

Create `threshold.py`:

```python
def breached(value, threshold):
    return value >= threshold
```

Create `test_threshold.py`:

```python
import unittest

import threshold


class TestThreshold(unittest.TestCase):
    def test_breached_true(self):
        self.assertTrue(threshold.breached(90, 80))

    def test_breached_false(self):
        self.assertFalse(threshold.breached(70, 80))


if __name__ == "__main__":
    unittest.main()
```

Run:

```bash
python3 test_threshold.py
```

Expected output (summary):

```text
OK
```

## Common Mistakes (With Errors)

### Mistake 1 — Wrong file name / import path

If Python can’t import your module:

```text
ModuleNotFoundError: No module named 'threshold'
```

Fix: run tests from the same folder as the module (or use a package layout).

### Mistake 2 — Tests depend on network/filesystem

Unit tests should be fast and predictable.

Fix: test pure logic, and separate “integration tests” for external systems.

## Quick Reference

- Create test case: `class X(unittest.TestCase)`
- Assertions: `assertTrue`, `assertFalse`, `assertEqual`
- Run: `python3 test_file.py`

## Next

Next: [Lesson 32 — Code Quality (formatting & linting)](32-code-quality-formatting-linting.md)
