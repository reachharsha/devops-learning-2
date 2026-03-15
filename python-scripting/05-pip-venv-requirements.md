---
title: "Python for DevOps Automation: 05 - pip, venv, requirements.txt"
render_with_liquid: false
---

# Lesson 05 — pip, venv, requirements.txt

## Objectives

- Understand pip
- Create and activate venv
- Use `requirements.txt`

## Real-world analogy

A venv is a separate toolbox for one project.

## Concepts

- pip installs packages
- venv isolates dependencies
- requirements.txt pins versions

## Hands-on Lab

```bash
mkdir -p devops-python
cd devops-python

python3 -m venv .venv
source .venv/bin/activate

python -m pip install requests
python -m pip freeze > requirements.txt
cat requirements.txt

python -m pip install -r requirements.txt
deactivate
```

## Common mistakes

- Installing globally instead of using venv
- Using `pip` that points to a different Python

Fix: prefer `python -m pip`.

## DevOps use case

CI/CD installs from `requirements.txt` to guarantee repeatable runs.

## Quick Reference

- Create venv: `python3 -m venv .venv`
- Activate: `source .venv/bin/activate`
- Freeze: `python -m pip freeze > requirements.txt`
- Install: `python -m pip install -r requirements.txt`

## Next

[Lesson 06: REPL, First Script, Shebang](06-repl-first-script-shebang.md)
