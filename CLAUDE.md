# ai-dev

Ubuntu WSL configuration for local AI model deployment with llama.cpp.

This repo is a starting point for configuring an Ubuntu WSL deployment to work with a local AI model leveraging llama.cpp. Ansible is used to automate provisioning and configuration.

## Project structure

- [pyproject.toml](pyproject.toml) — uv project with `ansible` and `ansible-lint` dependencies
- [uv.lock](uv.lock) — locked dependency graph
- [.venv/](.venv/) — Python 3.12 virtual environment (managed by uv)

## Setup

Install uv if not present:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
source $HOME/.local/bin/env
```

Install dependencies:

```bash
uv sync
```

## Running ansible

Always use `uv run` to invoke ansible tools so they run inside the managed venv — do not rely on system-level ansible installs.

```bash
uv run ansible --version
uv run ansible-playbook playbooks/<playbook>.yml
uv run ansible-lint playbooks/<playbook>.yml
uv run ansible-inventory --list
```

## Linting

Lint playbooks before running them:

```bash
uv run ansible-lint
```

## Adding dependencies

```bash
uv add <package>
```
