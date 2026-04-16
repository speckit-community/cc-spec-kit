# CC-Spec-Kit

> **Note:** This is a community-maintained Claude Code plugin port of [Spec Kit](https://github.com/github/spec-kit). It is not affiliated with or endorsed by GitHub.

A Claude Code / Copilot plugin for installing [Spec Kit](https://github.com/github/spec-kit).

### Why a plugin?

The Spec Kit project CLI tool requires Python. This plugin bundles the templates, scripts, and workflow as a native agent plugin, which means:

- **Native package management** — install, update, and remove like any other plugin from the Claude or Copilot CLI
- **CLI compatible** — projects initialized with the plugin are fully compatible with the `specify` CLI if you ever want to switch

## Installation

### Claude Code

```bash
claude plugin marketplace add speckit-community/cc-spec-kit
claude plugin install spec-kit@speckit-community
```

### GitHub Copilot CLI

```bash
copilot plugin install speckit-community/cc-spec-kit
```

## Updating

### Claude Code

```bash
claude plugin update spec-kit@speckit-community
```

### GitHub Copilot CLI

```bash
copilot plugin update speckit-community/cc-spec-kit
```

After updating the plugin, re-initialize your project to pick up the latest assets:

```
/speckit:init --force
```

## Quick Start

1. **Initialize** your project with Spec Kit infrastructure:
   ```
   /speckit:init
   ```

2. **Set up** your project constitution:
   ```
   /speckit-constitution
   ```

3. **Specify** a new feature:
   ```
   /speckit-specify <feature description>
   ```

4. **Plan** the implementation:
   ```
   /speckit-plan
   ```

5. **Generate tasks**:
   ```
   /speckit-tasks
   ```

6. **Implement**:
   ```
   /speckit-implement
   ```

## Available Skills

### Core Workflow

| Skill | Command | Description |
|-------|---------|-------------|
| init | `/speckit:init` | Initialize project with `.specify/` infrastructure |
| constitution | `/speckit-constitution` | Create or update the project constitution |
| specify | `/speckit-specify` | Create or update a feature specification |
| clarify | `/speckit-clarify` | Ask clarification questions about a spec |
| plan | `/speckit-plan` | Generate an implementation plan |
| tasks | `/speckit-tasks` | Generate dependency-ordered tasks |
| implement | `/speckit-implement` | Execute tasks from the implementation plan |

### Analysis & Quality

| Skill | Command | Description |
|-------|---------|-------------|
| analyze | `/speckit-analyze` | Cross-artifact consistency analysis |
| checklist | `/speckit-checklist` | Generate a quality checklist for requirements |
| taskstoissues | `/speckit-taskstoissues` | Convert tasks to GitHub issues |

### Git Integration

| Skill | Command | Description |
|-------|---------|-------------|
| git-commit | `/speckit-git-commit` | Auto-commit after a Spec Kit command |
| git-feature | `/speckit-git-feature` | Create a feature branch |
| git-initialize | `/speckit-git-initialize` | Initialize a Git repository |
| git-remote | `/speckit-git-remote` | Detect Git remote URL |
| git-validate | `/speckit-git-validate` | Validate feature branch naming |

## License

MIT
