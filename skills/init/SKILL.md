---
name: init
description: "Initialize .specify/ workspace by copying bundled assets from the plugin"
argument-hint: "Optional: --timestamp for timestamp-based branch numbering"
metadata:
  author: "github-spec-kit"
  source: "speckit-init"
user-invocable: true
disable-model-invocation: true
---

# Initialize SpecKit Workspace

## User Input

```text
$ARGUMENTS
```

## Purpose

Scaffold the `.specify/` workspace directory by copying all bundled assets from `${CLAUDE_PLUGIN_ROOT}/assets/` into the project root. After initialization, the project is ready for all workflow skills and is fully compatible with the specify CLI.

## Pre-Execution

No hooks — init has no before/after hooks.

## Execution

### Step 1: Check if `.specify/` already exists

- If `.specify/` does **not** exist → proceed to Step 2 (full scaffold)
- If `.specify/` already exists → proceed to Step 3 (idempotent update)

### Step 2: Full Scaffold (fresh project)

Copy the entire contents of `${CLAUDE_PLUGIN_ROOT}/assets/` into `.specify/` at the project root:

```
${CLAUDE_PLUGIN_ROOT}/assets/  →  .specify/
```

This creates the following structure:

```
.specify/
├── scripts/
│   ├── bash/           (5 scripts: common.sh, check-prerequisites.sh, create-new-feature.sh, setup-plan.sh, update-agent-context.sh)
│   └── powershell/     (5 scripts: common.ps1, check-prerequisites.ps1, create-new-feature.ps1, setup-plan.ps1, update-agent-context.ps1)
├── templates/          (6 templates: spec-template.md, plan-template.md, tasks-template.md, checklist-template.md, constitution-template.md, agent-file-template.md)
├── extensions/
│   ├── .registry
│   └── git/            (extension.yml, git-config.yml, config-template.yml, README.md, commands/, scripts/)
├── integrations/       (claude.manifest.json, speckit.manifest.json, claude/scripts/)
├── memory/
│   └── constitution.md
├── extensions.yml
├── init-options.json
└── integration.json
```

**Platform-specific steps**:
- **Unix (Linux/macOS)**: Run `chmod +x` on all `.sh` files under `.specify/scripts/bash/` and `.specify/extensions/git/scripts/bash/` and `.specify/integrations/claude/scripts/`
- **Windows**: No additional steps needed (PowerShell scripts don't need execute permission)

### Step 3: Idempotent Update (existing workspace)

When `.specify/` already exists:

1. Walk the `${CLAUDE_PLUGIN_ROOT}/assets/` directory tree
2. For each file in assets:
   - If the corresponding file does **NOT** exist in `.specify/` → copy it
   - If the corresponding file **DOES** exist in `.specify/` → **skip it** (do not overwrite)
3. On Unix: run `chmod +x` on any newly added `.sh` files
4. Report what was added vs. what was skipped

### Step 4: Handle `--timestamp` argument

If the user provided `--timestamp` in `$ARGUMENTS`:

1. Read `.specify/init-options.json`
2. Change `"branch_numbering"` from `"sequential"` to `"timestamp"`
3. Write the updated file back

### Step 5: Report Results

Output a summary:
- List of files/directories that were **created** (new)
- List of files that were **skipped** (already existed)
- Current `branch_numbering` setting
- Confirmation: "Workspace initialized. Ready for /cc-spec-kit-core:specify"

## Post-Execution

No hooks — init has no before/after hooks.
