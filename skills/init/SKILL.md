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
  - Continue to step 2 (existing directories will be overwritten by the copy).

- **If `.specify/` does not exist**:
  - Continue to step 2.

### 2. Detect Platform

Determine the user's operating system to select the correct asset variant.

Run a quick platform check:

```bash
uname -s 2>/dev/null || echo "Windows"
```

- **If the output contains `MINGW`, `MSYS`, `CYGWIN`, or `Windows`** → set `PLATFORM=ps`
- **Otherwise** (Darwin, Linux, etc.) → set `PLATFORM=bash`

### 3. Copy Infrastructure

Copy the `.specify/` and `.claude/` directories from the detected platform asset into the project root.

**For bash (macOS / Linux):**

```bash
cp -R "${CLAUDE_PLUGIN_ROOT}/assets/bash/.specify" .specify
cp -R "${CLAUDE_PLUGIN_ROOT}/assets/bash/.claude" .claude
```

**For ps (Windows):**

```powershell
Copy-Item -Recurse -Force "${CLAUDE_PLUGIN_ROOT}/assets/ps/.specify" .specify
Copy-Item -Recurse -Force "${CLAUDE_PLUGIN_ROOT}/assets/ps/.claude" .claude
```

### 4. Set Script Permissions (bash only)

If `PLATFORM=bash`, make all shell scripts executable:

```bash
find .specify -name '*.sh' -exec chmod +x {} +
```

Skip this step on Windows — PowerShell scripts do not need execute permission.

### 5. Report Summary

List what was installed:

```
✅ Spec Kit initialized successfully! (platform: <PLATFORM>)

Installed:
  .claude/skills/         — Claude Code skills for the Spec Kit workflow
  .specify/scripts/       — Workflow automation scripts
  .specify/templates/     — Templates for spec, plan, tasks, constitution, etc.
  .specify/extensions/    — Git extension with auto-commit hooks
  .specify/memory/        — Constitution and project memory
  .specify/integrations/  — Integration configuration

⚠️  Restart your session to pick up the new skills.

Next steps:
  1. Restart the session (exit and re-enter, or /reload-plugins)
  2. Set up your project constitution: /spec-kit:constitution
  3. Start your first feature spec:    /spec-kit:specify <description>
```
