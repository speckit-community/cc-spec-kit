---
name: "init"
description: "Initialize a new project with the Spec Kit workflow infrastructure. Copies .specify/ and .claude/ directories with scripts, templates, skills, and extensions."
argument-hint: "Use --force to overwrite an existing .specify/ directory"
user-invocable: true
disable-model-invocation: true
---

## User Input

```text
$ARGUMENTS
```

## Goal

Bootstrap a project with the Spec Kit workflow infrastructure by copying the `.specify/` and `.claude/` directories from the plugin into the user's project root.

## Execution Steps

### 1. Check for Existing Installation

Check if a `.specify/` directory already exists in the current working directory.

- **If `.specify/` exists and `$ARGUMENTS` does NOT contain `--force`**:
  - Print a warning:
    ```
    ⚠️  A .specify/ directory already exists in this project.
    To reinitialize, run: /spec-kit:init --force
    ```
  - **Stop execution. Do not proceed.**

- **If `.specify/` exists and `$ARGUMENTS` contains `--force`**:
  - Print: `Reinitializing Spec Kit (--force specified)...`
  - Remove the existing directories: `rm -rf .specify/ .claude/`
  - Continue to step 2.

- **If `.specify/` does not exist**:
  - Continue to step 2.

### 2. Copy Infrastructure

Copy the `.specify/` and `.claude/` directories from the plugin to the project root:

```bash
cp -R "${CLAUDE_PLUGIN_ROOT}/assets/bash/.specify" .specify
cp -R "${CLAUDE_PLUGIN_ROOT}/assets/bash/.claude" .claude
```

### 3. Set Script Permissions

Make all shell scripts executable:

```bash
find .specify -name '*.sh' -exec chmod +x {} +
```

### 4. Report Summary

List what was installed:

```
✅ Spec Kit initialized successfully!

Installed:
  .claude/skills/         — Claude Code skills for the Spec Kit workflow
  .specify/scripts/       — Shell scripts for workflow automation
  .specify/templates/     — Templates for spec, plan, tasks, constitution, etc.
  .specify/extensions/    — Git extension with auto-commit hooks
  .specify/memory/        — Constitution and project memory
  .specify/integrations/  — Integration configuration

Next steps:
  1. Set up your project constitution: /spec-kit:constitution
  2. Start your first feature spec:    /spec-kit:specify <description>
```
