# CC-Spec-Kit

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

## Quick Start

1. **Initialize** your project with Spec Kit infrastructure:
   ```
   /spec-kit:init
   ```

2. **Set up** your project constitution:
   ```
   /spec-kit:constitution
   ```

3. **Specify** a new feature:
   ```
   /spec-kit:specify <feature description>
   ```

4. **Plan** the implementation:
   ```
   /spec-kit:plan
   ```

5. **Generate tasks**:
   ```
   /spec-kit:tasks
   ```

6. **Implement**:
   ```
   /spec-kit:implement
   ```

## Available Skills

### Core Workflow

| Skill | Command | Description |
|-------|---------|-------------|
| init | `/spec-kit:init` | Initialize project with `.specify/` infrastructure |
| constitution | `/spec-kit:constitution` | Create or update the project constitution |
| specify | `/spec-kit:specify` | Create or update a feature specification |
| clarify | `/spec-kit:clarify` | Ask clarification questions about a spec |
| plan | `/spec-kit:plan` | Generate an implementation plan |
| tasks | `/spec-kit:tasks` | Generate dependency-ordered tasks |
| implement | `/spec-kit:implement` | Execute tasks from the implementation plan |

### Analysis & Quality

| Skill | Command | Description |
|-------|---------|-------------|
| analyze | `/spec-kit:analyze` | Cross-artifact consistency analysis |
| checklist | `/spec-kit:checklist` | Generate a quality checklist for requirements |
| taskstoissues | `/spec-kit:taskstoissues` | Convert tasks to GitHub issues |

### Git Integration

| Skill | Command | Description |
|-------|---------|-------------|
| git-commit | `/spec-kit:git-commit` | Auto-commit after a Spec Kit command |
| git-feature | `/spec-kit:git-feature` | Create a feature branch |
| git-initialize | `/spec-kit:git-initialize` | Initialize a Git repository |
| git-remote | `/spec-kit:git-remote` | Detect Git remote URL |
| git-validate | `/spec-kit:git-validate` | Validate feature branch naming |

## License

MIT
