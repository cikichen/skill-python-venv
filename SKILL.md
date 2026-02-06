---
name: python-venv
description: "Before running Python scripts or installing packages, you MUST use a virtual environment in the current working directory. This applies to: running .py files, using pip/uv pip install, or any task requiring third-party packages. Exceptions: simple one-liners using only Python standard library."
---

# Python Virtual Environment Requirement

## Core Rule

**Use virtual environment when installing packages or running scripts that require third-party dependencies.**

## When Virtual Environment is REQUIRED

| Scenario | Required? | Reason |
|----------|-----------|--------|
| `pip install` / `uv pip install` | ✅ YES | Installing packages |
| Running `.py` files with third-party imports | ✅ YES | Needs dependencies |
| `python script.py` with `requirements.txt` | ✅ YES | Project dependencies |
| Multi-file Python projects | ✅ YES | Isolation needed |

## When Virtual Environment is NOT Required

| Scenario | Required? | Example |
|----------|-----------|---------|
| Simple one-liner with stdlib only | ❌ NO | `python3 -c "print('hello')"` |
| Quick math/string operations | ❌ NO | `python3 -c "print(2**10)"` |
| Using only built-in modules | ❌ NO | `python3 -c "import json; ..."` |
| Checking Python version | ❌ NO | `python3 --version` |

### Python Standard Library (No venv needed)

These modules are built-in and don't require virtual environment:
```
os, sys, json, re, math, datetime, pathlib, subprocess, 
collections, itertools, functools, argparse, logging,
urllib, http, socket, threading, multiprocessing, etc.
```

## Workflow (When venv IS Required)

```
1. Check if .venv exists → If YES, activate and reuse it
2. If .venv does NOT exist → Create it, then activate
3. Proceed with Python commands
```

## Setup Methods (Choose One)

### Option 1: uv (Recommended - Faster)

```bash
# Create virtual environment
uv venv

# Activate it
source .venv/bin/activate

# Install packages
uv pip install <package>
```

### Option 2: Standard venv

```bash
# Create virtual environment
python3 -m venv .venv

# Activate it
source .venv/bin/activate

# Install packages
pip install <package>
```

## Workflow Checklist

Before ANY Python operation:

1. [ ] Check if `.venv` directory exists: `[ -d .venv ]`
2. [ ] If exists → **Reuse it**: `source .venv/bin/activate`
3. [ ] If not exists → Create: `uv venv` or `python3 -m venv .venv`
4. [ ] Activate: `source .venv/bin/activate`
5. [ ] Proceed with Python commands

**Priority: Always reuse existing `.venv` to preserve installed packages.**

## Quick Reference

| Task | Command |
|------|---------|
| Create venv (uv) | `uv venv` |
| Create venv (standard) | `python3 -m venv .venv` |
| Activate | `source .venv/bin/activate` |
| Install package (uv) | `uv pip install <pkg>` |
| Install package (pip) | `pip install <pkg>` |
| Install from requirements | `uv pip install -r requirements.txt` |
| Deactivate | `deactivate` |

## Common Patterns

### Standard Pattern (Reuse or Create)
```bash
# Check and reuse existing venv, or create new one
[ -d .venv ] && source .venv/bin/activate || (uv venv && source .venv/bin/activate)
```

### Running a Python Script
```bash
# Activate existing or create new
[ -d .venv ] && source .venv/bin/activate || (uv venv && source .venv/bin/activate)

# Install dependencies if needed
[ -f requirements.txt ] && uv pip install -r requirements.txt

# Run script
python script.py
```

### Quick One-off Script
```bash
[ -d .venv ] && source .venv/bin/activate || (uv venv && source .venv/bin/activate)
uv pip install pandas  # install needed packages
python my_script.py
```

### Check if venv is Active
```bash
# Should show path containing .venv
which python
```

## Forbidden Actions

- Using `pip install` with system Python (always use venv)
- Installing packages globally
- Assuming third-party packages are available without explicit installation

## Allowed Without venv

- `python3 -c "print('hello')"`
- `python3 -c "import os; print(os.getcwd())"`
- `python3 --version`
- Any stdlib-only one-liner
