# cc-spec-kit-core

A Claude Code plugin providing a structured feature development workflow: brainstorm → specify → clarify → plan → tasks → implement → checklist → analyze.

Ported from the upstream [SpecKit](https://github.com/spec-kit) project. Fully compatible with the `specify` CLI — projects initialized with this plugin work seamlessly with both tools.

## Installation

```bash
# Install from local directory
claude plugin install ./cc-spec-kit-core

# Or use --plugin-dir during development
claude --plugin-dir ./cc-spec-kit-core
```

## Quick Start

```
/cc-spec-kit-core:init                          # Initialize .specify/ workspace
/cc-spec-kit-core:specify "add user auth"       # Create feature specification
/cc-spec-kit-core:plan                          # Generate implementation plan
/cc-spec-kit-core:tasks                         # Break plan into tasks
/cc-spec-kit-core:implement                     # Execute tasks
```

## Available Skills

| Skill | Purpose |
|-------|---------|
| **init** | Scaffold `.specify/` workspace from bundled assets |
| **specify** | Create or update feature specification |
| **clarify** | Refine specification with targeted questions |
| **plan** | Generate implementation plan with research and contracts |
| **tasks** | Break plan into dependency-ordered tasks |
| **implement** | Execute implementation tasks from tasks.md |
| **checklist** | Generate quality checklists for requirements |
| **analyze** | Cross-artifact consistency analysis |
| **constitution** | Create/update project constitution |
| **tasks-to-issues** | Convert tasks to GitHub issues |
| **git-initialize** | Initialize git repository |
| **git-feature** | Create feature branch |
| **git-commit** | Auto-commit changes after skill completion |
| **git-validate** | Validate feature branch naming |
| **brainstorm** | Brainstorm ideas before specification |

## Full Workflow

```
init → constitution → specify → clarify → plan → tasks → implement → checklist → analyze
```

## Dual-Tool Compatibility

After `init`, the specify CLI works on the same project:

```bash
specify plan      # Uses the same .specify/ and specs/
specify tasks     # Works seamlessly
```

Both tools share the `.specify/` workspace and `specs/` feature directories.

## Architecture

The plugin bundles all upstream SpecKit assets under `assets/`. The `init` skill copies these into `.specify/` in the project root, creating a workspace identical to one produced by `specify init --here --ai claude`.

After initialization, all skills reference `.specify/` paths directly — no runtime dependency on the plugin bundle.

### Extension Packaging Pattern

SpecKit extensions can be packaged as separate Claude Code plugins:

1. **Map extension.yml → plugin.json**: Extension metadata becomes plugin manifest fields
2. **Map commands → skills**: Each extension command becomes a `skills/<name>/SKILL.md`
3. **Register hooks**: Use a SessionStart hook to merge extension hooks into `.specify/extensions.yml`

The bundled `git` extension demonstrates this pattern. See `assets/extensions/git/` for reference.

For external extensions, the plugin structure is:

```
<extension-plugin>/
├── .claude-plugin/plugin.json
├── skills/<command>/SKILL.md      # One per extension command
├── assets/
│   ├── extension.yml
│   └── scripts/{bash,powershell}/
└── README.md
```

## Development

### Repository Structure

```
cc-spec-kit-core/             # The plugin package
├── .claude-plugin/plugin.json
├── skills/                   # 15 skills
├── hooks/                    # SessionStart hook
├── assets/                   # Bundled upstream assets
│   ├── scripts/              # Core bash + PowerShell scripts
│   ├── templates/            # Markdown templates
│   ├── extensions/git/       # Git extension
│   ├── integrations/         # Integration configs
│   └── ...
└── README.md
```

### Running Tests

```bash
# From the dev repo root
python3 -m pytest tests/ -v
```

### Cross-Platform Support

All scripts exist in both bash (Linux/macOS) and PowerShell (Windows) variants. Skills reference both variants for OS-based selection at runtime.