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

## How This Plugin Is Generated

This plugin is a community-maintained port of [Spec Kit](https://github.com/github/spec-kit). The plugin assets are **generated** from the upstream `specify` CLI and kept in sync automatically as upstream evolves.

### Generation process

1. For each variant (bash, PowerShell), `specify init` is run with the appropriate flags.
2. The resulting `.claude/` and `.specify/` directories are copied into the corresponding `assets/{bash,ps}/` folder.

### Staying aligned with upstream

A [GitHub Actions workflow](/.github/workflows/update-speckit-assets.yml) runs daily to keep the plugin in sync:

1. **Detect** — the workflow checks the [latest stable release](https://github.com/github/spec-kit/releases) of `github/spec-kit` and compares it to the version in `.claude-plugin/plugin.json`. Pre-release versions (dev, alpha, beta, rc) are skipped.
2. **Regenerate** — if a newer stable release is found, both asset variants are regenerated from scratch.
3. **Bump** — `.claude-plugin/plugin.json` is updated to reflect the new version.
4. **PR** — the workflow opens a pull request (e.g., `auto/update-speckit-<version>`) with the regenerated assets and version bump for review before merging.

This means the plugin tracks upstream releases automatically — maintainers only need to review and merge the auto-generated PRs.

## License

MIT
