# OpenCode Skill: Python Virtual Environment

Enforce virtual environment usage for Python projects that require third-party packages.

[中文说明](#中文说明)

## Features

- ✅ Require venv when installing packages or using third-party dependencies
- ✅ Reuse existing virtual environment (`.venv`, `venv`, `env`, `.env`)
- ✅ Auto-create if not exists
- ✅ Support `uv` (recommended) with fallback to standard `venv`
- ✅ Support Conda/Mamba environments
- ✅ Cross-platform (Linux, macOS, Windows)
- ✅ **Skip venv for simple stdlib-only commands**

## When venv is Required

| Scenario | Required? |
|----------|-----------|
| `pip install` / `uv pip install` | ✅ YES |
| Running scripts with third-party imports | ✅ YES |
| Projects with `requirements.txt` / `pyproject.toml` | ✅ YES |

## When venv is NOT Required

| Scenario | Example |
|----------|---------|
| Simple stdlib one-liner | `python3 -c "print('hello')"` |
| Built-in modules only | `python3 -c "import json; ..."` |
| Version check | `python3 --version` |

## Installation

```bash
cd ~/.config/opencode/skills
git clone https://github.com/cikichen/opencode-skill-python-venv.git python-venv
```

## Quick Reference

### Linux/macOS
```bash
# Reuse existing or create new (with uv fallback to venv)
[ -d .venv ] && source .venv/bin/activate || { command -v uv &>/dev/null && uv venv || python3 -m venv .venv; source .venv/bin/activate; }
```

### Windows PowerShell
```powershell
if (Test-Path .venv) { .\.venv\Scripts\Activate.ps1 }
elseif (Get-Command uv -ErrorAction SilentlyContinue) { uv venv; .\.venv\Scripts\Activate.ps1 }
else { python -m venv .venv; .\.venv\Scripts\Activate.ps1 }
```

## Project Type Detection

| File | Install Command |
|------|-----------------|
| `requirements.txt` | `pip install -r requirements.txt` |
| `pyproject.toml` | `pip install -e .` |
| `environment.yml` | `conda env create -f environment.yml` |

---

## 中文说明

为需要第三方包的 Python 项目强制使用虚拟环境。

### 功能

- ✅ 安装包或使用第三方依赖时必须使用 venv
- ✅ 复用现有虚拟环境（`.venv`、`venv`、`env`、`.env`）
- ✅ 不存在时自动创建
- ✅ 支持 `uv`（推荐），自动 fallback 到标准 `venv`
- ✅ 支持 Conda/Mamba 环境
- ✅ 跨平台（Linux、macOS、Windows）
- ✅ **简单的标准库命令可跳过 venv**

### 何时需要 venv

| 场景 | 需要? |
|------|-------|
| `pip install` / `uv pip install` | ✅ 是 |
| 运行使用第三方库的脚本 | ✅ 是 |
| 有 `requirements.txt` / `pyproject.toml` 的项目 | ✅ 是 |

### 何时不需要 venv

| 场景 | 示例 |
|------|------|
| 简单的标准库单行命令 | `python3 -c "print('hello')"` |
| 仅使用内置模块 | `python3 -c "import json; ..."` |
| 版本检查 | `python3 --version` |

### 安装

```bash
cd ~/.config/opencode/skills
git clone https://github.com/cikichen/opencode-skill-python-venv.git python-venv
```

### 项目类型检测

| 文件 | 安装命令 |
|------|----------|
| `requirements.txt` | `pip install -r requirements.txt` |
| `pyproject.toml` | `pip install -e .` |
| `environment.yml` | `conda env create -f environment.yml` |

## License

MIT
