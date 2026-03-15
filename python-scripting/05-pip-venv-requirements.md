---
title: "Python for DevOps Automation: 05 - pip, venv, requirements.txt"
render_with_liquid: false
---

# Lesson 05 — pip, venv, requirements.txt

## Objectives

By the end, you can:

- Explain what a **package** and a **dependency** are
- Install packages using `pip` (the safe way)
- Create and activate a virtual environment (`venv`)
- Generate and use `requirements.txt` for repeatable installs (CI/CD)

## Real-world analogy

Think of a virtual environment (venv) as a **separate toolbox per project**.

- If every project uses one shared system Python, tools (packages) clash.
- If each project has its own venv, each project gets the exact tools it needs.

## Concepts

### What is a package?

A **package** is reusable code someone else wrote, distributed so you can install it.

Example: `requests` helps your script call HTTP APIs.

### What is a dependency?

A **dependency** is a package your project needs to run.

If your script imports `requests`, then `requests` is a dependency.

### What is pip?

`pip` is the package installer for Python.

It downloads and installs packages into *a specific Python environment*.

### What is venv?

`venv` creates an isolated Python environment in a folder (commonly `.venv/`).

When the venv is active:

- `python` points to the venv interpreter
- packages install into the venv (not globally)

### What is requirements.txt?

`requirements.txt` is a list of packages + versions.

CI/CD uses it so installs are repeatable:

```bash
python -m pip install -r requirements.txt
```

## Hands-on Lab

You’ll create a project folder, create a venv, install a dependency, and freeze versions.

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

### Understand what happened

- `.venv/` now contains a Python interpreter and its own `site-packages/`
- `requests` (and its dependencies) were installed into that venv
- `requirements.txt` captured the versions so you can reinstall later

### Verify you are using the venv (do this often)

With the venv activated:

```bash
which python
python -c "import sys; print(sys.executable)"
python -m pip --version
```

You should see paths that include `.venv`.

## Common mistakes

### Mistake 1 — Installing globally by accident

If you forget to activate the venv, you might pollute system Python.

Fix: `source .venv/bin/activate` before installing.

### Mistake 2 — Using the wrong pip

This happens when `pip` installs into one Python, but you run another Python.

Fix: prefer:

```bash
python -m pip install ...
```

### Mistake 3 — Dependency drift

If you don’t pin versions, installs can change over time.

Fix: freeze to `requirements.txt` and install from it in CI.

## DevOps use case

Your laptop and your CI runner should install the same dependencies.

This is the basic workflow:

1) create venv
2) install dependencies
3) freeze requirements
4) CI installs from `requirements.txt`

## Quick Reference

- Create venv: `python3 -m venv .venv`
- Activate: `source .venv/bin/activate`
- Verify active Python: `python -c "import sys; print(sys.executable)"`
- Freeze: `python -m pip freeze > requirements.txt`
- Install: `python -m pip install -r requirements.txt`

## Next

[Lesson 06: REPL, First Script, Shebang](06-repl-first-script-shebang.md)
