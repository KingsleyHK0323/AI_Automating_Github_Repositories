<div align="center">

  <h1>🤖 Automating GitHub Repositories</h1>

  <p>
    <b>A standardized AI Agent Skill for architecting, validating, and deploying secure GitHub Actions, CI/CD pipelines, and autonomous repository workflows.</b>
  </p>

  <p>
    <img src="https://img.shields.io/github/license/KingsleyHK0323/AI_Automating_Github_Repositories?style=for-the-badge" alt="License: MIT" />
    <img src="https://img.shields.io/badge/Format-SKILL.md-blue?style=for-the-badge" alt="Format: SKILL.md" />
    <img src="https://img.shields.io/badge/Version-1.2.0-green?style=for-the-badge" alt="Version: 1.2.0" />
    <img src="https://img.shields.io/badge/Actions-GitHub_Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white" alt="GitHub Actions" />
  </p>

  <p>
    <a href="#overview">Overview</a> •
    <a href="#core-capabilities">Capabilities</a> •
    <a href="#standard-workflow-templates">Templates</a> •
    <a href="#installation">Installation</a> •
    <a href="#usage">Usage</a> •
    <a href="#security-standards">Security</a> •
    <a href="#repository-structure">Structure</a> •
    <a href="#contributing">Contributing</a> •
    <a href="#changelog">Changelog</a> •
    <a href="#license">License</a>
  </p>

</div>

<hr />

## Overview

**Automating GitHub Repositories** is a production-ready `SKILL.md` specification that equips AI coding assistants with structured DevOps patterns for configuring, hardening, and deploying GitHub Actions automation. It enforces least-privilege `GITHUB_TOKEN` permissions, script-injection protections, and verified YAML templates so AI agents generate workflows that execute cleanly without syntax errors or security vulnerabilities.

> [!IMPORTANT]
> **Core Principle:** Automate testing, scheduling, and repository maintenance using least-privilege permissions, deterministic triggers, and zero hardcoded secrets.

<hr />

## Core Capabilities

<table>
  <tr>
    <td width="50%">
      <h3>⚙️ CI/CD Pipelines</h3>
      <p>Automates unit testing, static linting, dependency caching, and multi-platform builds on every <code>push</code> and <code>pull_request</code>.</p>
    </td>
    <td width="50%">
      <h3>🕒 Scheduled Cron Jobs</h3>
      <p>Configures POSIX <code>cron</code> schedules with <code>workflow_dispatch</code> triggers for periodic API polling, backups, and self-committing updates.</p>
    </td>
  </tr>
  <tr>
    <td width="50%">
      <h3>🛠️ Repository Maintenance</h3>
      <p>Standardizes Dependabot security scanning, automated issue/PR labeling, and loop-safe auto-commit workflows (<code>[skip ci]</code>).</p>
    </td>
    <td width="50%">
      <h3>🔒 Security Hardening</h3>
      <p>Enforces explicit <code>permissions</code> blocks, environment-variable sanitization against expression injection, and pinned action versions.</p>
    </td>
  </tr>
</table>

<hr />

## Standard Workflow Templates

<details>
<summary><b>1. Scheduled Repository Sync & Auto-Commit (<code>.github/workflows/automation.yml</code>)</b></summary>

```yaml
name: Automated Repository Sync and Task

on:
  schedule:
    - cron: '0 8 * * *' # Daily at 08:00 UTC
  workflow_dispatch:

permissions:
  contents: write

concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true

jobs:
  execute-automation:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Set Up Python Environment
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'
          cache: 'pip'

      - name: Install Dependencies
        run: |
          python -m pip install --upgrade pip
          if [ -f requirements.txt ]; then pip install -r requirements.txt; fi

      - name: Run Automation Script
        env:
          API_KEY: ${{ secrets.API_KEY }}
        run: python scripts/main.py

      - name: Commit and Push Changes
        uses: stefanzweifel/git-auto-commit-action@v5
        with:
          commit_message: "chore: autonomous repository update [skip ci]"
          branch: main
```

</details>

<details>
<summary><b>2. Continuous Integration Pipeline (<code>.github/workflows/ci.yml</code>)</b></summary>

```yaml
name: Continuous Integration

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

permissions:
  contents: read

concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true

jobs:
  lint-and-test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Set Up Environment
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'
          cache: 'pip'

      - name: Install Dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt

      - name: Run Linter and Tests
        run: |
          ruff check .
          pytest
```

</details>

<hr />

## Installation

This repository distributes a standalone skill named `automating-github-repositories`. Clone the repository first:

```bash
git clone [https://github.com/KingsleyHK0323/AI_Automating_Github_Repositories.git](https://github.com/KingsleyHK0323/AI_Automating_Github_Repositories.git)
cd AI_Automating_Github_Repositories
```

Install `SKILL.md` into your preferred AI assistant environment:

<details>
<summary><b>Claude Code (CLI)</b></summary>

Copy `SKILL.md` into your global or project-level skills directory under a matching folder name:

```bash
# Global installation
mkdir -p ~/.claude/skills/automating-github-repositories
cp SKILL.md ~/.claude/skills/automating-github-repositories/SKILL.md

# Or project-scoped installation
mkdir -p .claude/skills/automating-github-repositories
cp SKILL.md .claude/skills/automating-github-repositories/SKILL.md
```

</details>

<details>
<summary><b>Claude (Web & Desktop Apps)</b></summary>

Compress the `automating-github-repositories` folder containing `SKILL.md` into a `.zip` archive and upload it via **Settings → Capabilities / Skills**. Refer to Anthropic's documentation for current UI steps.

</details>

<details>
<summary><b>Cursor, Gemini, ChatGPT, and Custom Agents</b></summary>

For tools that do not natively ingest `SKILL.md` files, copy the Markdown body of `SKILL.md` (everything below the closing `---` YAML frontmatter delimiter) into your project's rules file (e.g., `.cursor/rules`), Gems/Custom Instructions, or system prompt.

</details>

<hr />

## Usage

Once active, describe your automation requirement in plain language:

```text
Create a GitHub Actions CI workflow for this Python repository that runs ruff
and pytest on every push and pull request to main.
```

```text
Set up a daily scheduled workflow at 00:00 UTC that runs scripts/fetch_data.py
and commits updated JSON files back to main without triggering infinite CI loops.
```

The assistant generates the exact workflow files with least-privilege permissions, followed by a checklist of required repository secrets and placeholders.

<hr />

## Security Standards

| Rule | Implementation Enforced by Skill |
|---|---|
| **Least-Privilege Token** | Always defines explicit `permissions:` (`contents: read` by default; `contents: write` only when committing). |
| **Injection Prevention** | Prohibits direct `${{ github.event.* }}` interpolation inside `run:` scripts; requires `env:` mapping. |
| **Loop Prevention** | Appends `[skip ci]` to autonomous commit messages to prevent recursive workflow triggers. |
| **Version Pinning** | Uses verified major action tags (`@v4`, `@v5`) or commit SHAs instead of mutable `@main` branches. |
| **Secret Isolation** | References `${{ secrets.<NAME> }}` and flags any hardcoded credentials during validation. |

See [`SKILL.md`](SKILL.md) for the complete specification and pre-delivery checklist.

<hr />

## Repository Structure

```text
.
├── SKILL.md      # Standard AI skill specification (frontmatter, rules, workflow templates, checklist)
├── README.md     # Repository documentation, templates, and installation guide
└── LICENSE       # MIT License
```

<hr />

## Contributing

Contributions are welcome, especially new ecosystem templates and updated GitHub Actions security practices.

1. Fork the repository and create a feature branch (`git checkout -b feat/add-rust-ci-template`).
2. Update `SKILL.md` (and `README.md` if user-facing behavior changes), preserving valid YAML frontmatter (`name` and `description`).
3. Verify that all YAML templates pass syntax validation and follow least-privilege permission rules.
4. Open a pull request describing your changes.

<hr />

## Changelog

<details>
<summary><b>v1.2.0 (2026-11-22)</b></summary>

- Repaired truncated YAML blocks and unclosed HTML tags in `SKILL.md` and `README.md`.
- Standardized `SKILL.md` with complete YAML frontmatter (`license`, `metadata`), activation criteria, security hardening rules, CI/Dependabot templates, and a pre-delivery quality checklist.
- Updated `README.md` navigation anchors, multi-platform installation instructions, security reference table, and repository structure.

</details>

<details>
<summary><b>v1.0.0</b></summary>

- Initial release of `automating-github-repositories` skill and scheduled auto-commit workflow template.

</details>

<hr />

## License

Released under the [MIT License](LICENSE). Copyright (c) 2026 Kingsley ([@KingsleyHK0323](https://github.com/KingsleyHK0323)).