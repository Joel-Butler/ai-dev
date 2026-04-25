# ai-dev

Ubuntu WSL configuration for local AI model deployment with llama.cpp.

This repo is a starting point for configuring an Ubuntu WSL deployment to work with a local AI model leveraging llama.cpp. Ansible is used to automate provisioning and configuration.

## Project structure

- [pyproject.toml](pyproject.toml) — uv project with `ansible` and `ansible-lint` dependencies
- [uv.lock](uv.lock) — locked dependency graph
- [.venv/](.venv/) — Python 3.12 virtual environment (managed by uv)
- [inventory/hosts.yml](inventory/hosts.yml) — Ansible inventory (localhost, local connection)
- [playbooks/llama_cpp.yml](playbooks/llama_cpp.yml) — clone or pull llama.cpp into `~/dev/llama.cpp`

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
uv run ansible-playbook -i inventory/hosts.yml playbooks/<playbook>.yml
uv run ansible-lint playbooks/<playbook>.yml
uv run ansible-inventory -i inventory/hosts.yml --list
```

### Run the llama.cpp playbook

```bash
uv run ansible-playbook -i inventory/hosts.yml playbooks/llama_cpp.yml
```

## Ansible conventions

- Use `ansible_facts["fact_name"]` style (no `ansible_` prefix on the fact name) rather than the legacy bare `ansible_*` variables. Example: `ansible_facts["env"]["HOME"]` not `ansible_env.HOME`.

## Linting

Lint playbooks before running them:

```bash
uv run ansible-lint
```

## Adding dependencies

```bash
uv add <package>
```
