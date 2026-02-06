---
name: python-venv
description: "MANDATORY for ANY Python usage. Before running any Python code, scripts, or installing packages, you MUST create and activate a virtual environment in the current working directory using uv or venv. This applies to: running .py files, using pip/uv pip install, executing python -c commands, or any task requiring Python packages. Never use system Python directly."
---

# Python Virtual Environment Requirement

## Core Rule

**NEVER run Python code or install packages without first ensuring a virtual environment is active in the current working directory.**

## Workflow (MUST FOLLOW)

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

- Running `python` or `python3` without activating venv first
- Using `pip install` with system Python
- Installing packages globally
- Assuming packages are available without explicit installation
