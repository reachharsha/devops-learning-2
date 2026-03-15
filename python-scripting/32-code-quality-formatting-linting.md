---
title: "Python for DevOps Automation: 32 - Code Quality (formatting & linting)"
render_with_liquid: false
---

# Lesson 32 — Code Quality (Formatting & Linting)

As your scripts grow, consistency matters.

Code quality tools help you:

- keep code readable
- catch common mistakes early
- reduce bugs before production

## Objectives

- Understand formatting vs linting
- Use `ruff` (fast linter) and `black` (formatter) (optional)
- Learn a few high-impact style habits without tools

## Mental Model

- Formatter = automatic “tidy up the room” robot
- Linter = strict reviewer that points out issues

## Tools (optional but recommended)

Install inside your venv:

```bash
python3 -m pip install ruff black
```

Format with black:

```bash
black .
```

Lint with ruff:

```bash
ruff check .
```

## High-impact habits (even without tools)

- Use meaningful names: `error_count` not `x`
- Keep functions small and single-purpose
- Validate inputs near the top
- Prefer `pathlib` for paths
- Always set timeouts on network calls

## Common Mistakes

### Mistake 1 — Installing tools globally, not in venv

Fix: activate venv first, then install.

### Mistake 2 — Fighting the formatter

Fix: accept the formatter’s style; it saves time.

## Quick Reference

- Install: `pip install ruff black`
- Format: `black .`
- Lint: `ruff check .`

## Next

Next: [Lesson 33 — Mini Project 1 (Log Analyzer CLI)](33-mini-project-log-analyzer-cli.md)
