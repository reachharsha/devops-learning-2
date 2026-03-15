---
title: "Python for DevOps Automation: 01 - What Is Programming?"
render_with_liquid: false
---

# Lesson 01 — What Is Programming?

## Objectives

- Understand what programming means (plain language)
- Understand what a programming language is
- Learn script vs program vs application (DevOps context)
- Learn what syntax and algorithm mean

## Real-world analogy

Think of a computer like a very fast worker who:

- follows instructions **exactly**
- does not guess what you meant

Programming is writing **clear instructions**.

## Concepts (from scratch)

### Programming language

A programming language is a set of words + rules that lets you write instructions.

Python is popular for DevOps because it’s:

- readable
- has a huge standard library
- great for automation glue

### Script vs program vs application

- **Script**: small automation file you run (`python3 something.py`)
- **Program**: general term for code that runs
- **Application**: usually bigger (web app, desktop app)

In DevOps you mostly write scripts and small tools.

### Syntax

Syntax is the “grammar” of the language.

If you break syntax, Python stops with a `SyntaxError`.

### Algorithm

An algorithm is a step-by-step method.

Daily-life algorithm example (coffee):

1) boil water
2) add coffee
3) wait
4) pour

Automation scripts are algorithms for computers.

## Hands-on Lab (no code yet)

Write an automation algorithm in English:

Goal: “Alert when disk usage is high”.

Steps:

1) run a command to get disk usage
2) parse output
3) if usage > 80% then alert

## Common mistakes

- Trying to memorize everything
- Copy/paste code without reading errors

## DevOps use case

DevOps automation is mostly:

- read input (logs, APIs, files)
- make decisions
- take actions

## Quick Reference

- Programming: writing exact instructions
- Syntax: code grammar rules
- Algorithm: step-by-step method
- Script: small automation file

## Next

[Lesson 02: How Computers Run Python](02-how-computers-run-python.md)
