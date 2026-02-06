# OpenCode Skill: Python Virtual Environment

Enforce virtual environment usage for Python projects that require third-party packages.

[中文说明](#中文说明)

## Features

- ✅ Require venv when installing packages or using third-party dependencies
- ✅ Reuse existing `.venv` directory if present
- ✅ Auto-create if not exists
- ✅ Support `uv` (recommended, faster) and standard `venv`
- ✅ **Skip venv for simple stdlib-only commands**

## When venv is Required

| Scenario | Required? |
|----------|-----------|
| `pip install` / `uv pip install` | ✅ YES |
| Running scripts with third-party imports | ✅ YES |
| Projects with `requirements.txt` | ✅ YES |

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

```bash
# Standard pattern: reuse or create (when venv IS needed)
[ -d .venv ] && source .venv/bin/activate || (uv venv && source .venv/bin/activate)

# Install dependencies
uv pip install -r requirements.txt

# Run script
python script.py
```

---

## 中文说明

为需要第三方包的 Python 项目强制使用虚拟环境。

### 功能

- ✅ 安装包或使用第三方依赖时必须使用 venv
- ✅ 优先复用现有 `.venv` 目录
- ✅ 不存在时自动创建
- ✅ 支持 `uv`（推荐，更快）和标准 `venv`
- ✅ **简单的标准库命令可跳过 venv**

### 何时需要 venv

| 场景 | 需要? |
|------|-------|
| `pip install` / `uv pip install` | ✅ 是 |
| 运行使用第三方库的脚本 | ✅ 是 |
| 有 `requirements.txt` 的项目 | ✅ 是 |

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

## License

MIT
