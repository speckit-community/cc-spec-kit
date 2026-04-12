# cc-spec-kit-core

A Claude Code plugin for specification-driven development workflows. Provides skills for feature specification, planning, task generation, implementation, and analysis.

## Installation

### Development / Local Testing

```bash
claude --plugin-dir ./cc-spec-kit-core
```

### From a Marketplace

```bash
claude plugin install spec-kit
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

| Skill | Command | Description |
|-------|---------|-------------|
| init | `/spec-kit:init` | Initialize project with `.specify/` infrastructure |
| specify | `/spec-kit:specify` | Create or update a feature specification |
| clarify | `/spec-kit:clarify` | Ask clarification questions about a spec |
| plan | `/spec-kit:plan` | Generate an implementation plan |
| tasks | `/spec-kit:tasks` | Generate dependency-ordered tasks |
| implement | `/spec-kit:implement` | Execute tasks from the implementation plan |
| analyze | `/spec-kit:analyze` | Cross-artifact consistency analysis |
| checklist | `/spec-kit:checklist` | Generate a custom checklist |
| constitution | `/spec-kit:constitution` | Create or update the project constitution |
| taskstoissues | `/spec-kit:taskstoissues` | Convert tasks to GitHub issues |
| git-commit | `/spec-kit:git-commit` | Auto-commit after a Spec Kit command |
| git-feature | `/spec-kit:git-feature` | Create a feature branch |
| git-initialize | `/spec-kit:git-initialize` | Initialize a Git repository |
| git-remote | `/spec-kit:git-remote` | Detect Git remote URL |
| git-validate | `/spec-kit:git-validate` | Validate feature branch naming |

## Plugin Structure

```
cc-spec-kit-core/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest
├── skills/                   # All plugin skills
│   ├── init/
│   ├── specify/
│   ├── clarify/
│   ├── plan/
│   ├── tasks/
│   ├── implement/
│   ├── analyze/
│   ├── checklist/
│   ├── constitution/
│   ├── taskstoissues/
│   ├── git-commit/
│   ├── git-feature/
│   ├── git-initialize/
│   ├── git-remote/
│   └── git-validate/
└── .specify/                 # Bundled infrastructure (copied by init)
    ├── scripts/
    ├── templates/
    ├── extensions/
    ├── memory/
    └── integrations/
```

## License

MIT