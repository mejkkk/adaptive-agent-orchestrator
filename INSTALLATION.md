# Installation — Adaptive Agent Orchestrator

**Version 1.0 — Released** · [ภาษาไทย](INSTALLATION.th.md) · [Repository](https://github.com/mejkkk/adaptive-agent-orchestrator)

Install the **source directory** `skill/adaptive-agent-orchestrator/` from GitHub. No prebuilt package is required.

## 1. Prerequisites

- Git installed and available in the terminal.
- Codex, Claude Code, or Antigravity with Skills enabled.
- Permission to create a Skills directory in the target project.
- Required native Subagent capability and model access if you plan to use delegated execution.

Source layout:

```text
adaptive-agent-orchestrator/
└── skill/
    └── adaptive-agent-orchestrator/
        ├── SKILL.md
        ├── agents/
        │   └── openai.yaml
        └── references/
            ├── strategy-and-approval.md
            ├── execution-contracts.md
            └── verification-and-escalation.md
```

## 2. Installation locations

| Platform | Project-level destination | User/global destination | Invoke |
|---|---|---|---|
| Codex CLI / IDE | `<project>/.agents/skills/adaptive-agent-orchestrator/` | `~/.agents/skills/adaptive-agent-orchestrator/` | `$adaptive-agent-orchestrator` |
| Claude Code | `<project>/.claude/skills/adaptive-agent-orchestrator/` | `~/.claude/skills/adaptive-agent-orchestrator/` | `/adaptive-agent-orchestrator` |
| Antigravity IDE | `<project>/.agents/skills/adaptive-agent-orchestrator/` | Runtime/version dependent | `/adaptive-agent-orchestrator` when available |

Codex and Antigravity may share a project-level `.agents/skills` path. Check the installed application's current Skills documentation for supported global paths and invocation commands.

## 3. Clone source repository

**macOS / Linux (Bash)**

```bash
mkdir -p ~/agent-skill-sources
cd ~/agent-skill-sources
git clone https://github.com/mejkkk/adaptive-agent-orchestrator.git
```

**Windows (PowerShell)**

```powershell
New-Item -ItemType Directory -Force "$HOME\agent-skill-sources" | Out-Null
Set-Location "$HOME\agent-skill-sources"
git clone https://github.com/mejkkk/adaptive-agent-orchestrator.git
```

If you already cloned this repository, update with `git pull` instead of cloning again.

## 4. Install in your project

Replace `/path/to/your-project` with your actual project path.

**macOS / Linux (Bash)**

```bash
SOURCE="$HOME/agent-skill-sources/adaptive-agent-orchestrator/skill/adaptive-agent-orchestrator"
PROJECT="/path/to/your-project"

# Codex and Antigravity
mkdir -p "$PROJECT/.agents/skills"
cp -R "$SOURCE" "$PROJECT/.agents/skills/"

# Claude Code
mkdir -p "$PROJECT/.claude/skills"
cp -R "$SOURCE" "$PROJECT/.claude/skills/"
```

**Windows (PowerShell)**

```powershell
$Source = Join-Path $HOME "agent-skill-sources\adaptive-agent-orchestrator\skill\adaptive-agent-orchestrator"
$Project = "C:\path\to\your-project"

# Codex and Antigravity
$Dest = Join-Path $Project ".agents\skills\adaptive-agent-orchestrator"
New-Item -ItemType Directory -Force $Dest | Out-Null
Copy-Item -Path (Join-Path $Source '*') -Destination $Dest -Recurse -Force

# Claude Code
$ClaudeDest = Join-Path $Project ".claude\skills\adaptive-agent-orchestrator"
New-Item -ItemType Directory -Force $ClaudeDest | Out-Null
Copy-Item -Path (Join-Path $Source '*') -Destination $ClaudeDest -Recurse -Force
```

Install only the destination appropriate for the tools you actually use. Global installations use the user directory in the table above instead of a project path.

## 5. Update using git pull

A source repository `git pull` updates only the source checkout. **If you copied the Skill into a project, copy the updated folder again.**

**macOS / Linux (Bash)**

```bash
cd ~/agent-skill-sources/adaptive-agent-orchestrator
git pull --ff-only origin main

SOURCE="$HOME/agent-skill-sources/adaptive-agent-orchestrator/skill/adaptive-agent-orchestrator"
PROJECT="/path/to/your-project"
mkdir -p "$PROJECT/.agents/skills" "$PROJECT/.claude/skills"
cp -R "$SOURCE" "$PROJECT/.agents/skills/"
cp -R "$SOURCE" "$PROJECT/.claude/skills/"
```

**Windows (PowerShell)**

```powershell
Set-Location "$HOME\agent-skill-sources\adaptive-agent-orchestrator"
git pull --ff-only origin main

$Source = Join-Path $HOME "agent-skill-sources\adaptive-agent-orchestrator\skill\adaptive-agent-orchestrator"
$Project = "C:\path\to\your-project"

$Dest = Join-Path $Project ".agents\skills\adaptive-agent-orchestrator"
New-Item -ItemType Directory -Force $Dest | Out-Null
Copy-Item -Path (Join-Path $Source '*') -Destination $Dest -Recurse -Force

$ClaudeDest = Join-Path $Project ".claude\skills\adaptive-agent-orchestrator"
New-Item -ItemType Directory -Force $ClaudeDest | Out-Null
Copy-Item -Path (Join-Path $Source '*') -Destination $ClaudeDest -Recurse -Force
```

If your installed copy contains local customizations, back them up before overwriting. For exact synchronization, review and remove obsolete installed files manually; a copy does not automatically delete them.

## 6. Verify installation

Confirm the Skill entrypoint and references are present at `.../skills/adaptive-agent-orchestrator/SKILL.md`. Avoid accidentally nesting the directory twice.

Restart the agent session or reload Skills if necessary. Check its Skills list/customizations or invoke explicitly.

## 7. Invocation

Prepare requirements and/or an implementation plan before activating the Skill.

### Standard prompt template

```text
/adaptive-agent-orchestrator

Execute based on: <requirements.md or implementation-plan.md>

<Optional Overrides>
Model Preference: <optional model and effort preference>
Additional Instructions: <optional task-specific instructions>
```

The **Optional Overrides** block may be omitted entirely. Use the supplied requirements and/or implementation plan as the input; project-specific task requirements are not stored in the Skill.

### Example 1 — Standard execution (no overrides)

```text
/adaptive-agent-orchestrator

Execute based on: implementation-plan.md
```

The Lead reviews the available plan and requirements, breaks down tasks and dependencies, recommends SOLO or Subagents, and presents the execution strategy for approval.

### Example 2 — Execution with overrides

```text
/adaptive-agent-orchestrator

Execute based on:
- requirements.md
- implementation-plan.md

Model Preference: Prefer Luna with Max Effort.

Additional Instructions:
- Prioritize security verification.
- Do not deploy to production.
```

`Prefer Luna with Max Effort` is a **preference**, not a fixed model constraint; the Lead may justify other supported settings. `Do not deploy to production` is a **hard restriction**. Verification is prioritized as requested. Runtime model and effort availability must be checked.

**Platform note:** Examples use `/adaptive-agent-orchestrator` for Claude Code and Antigravity where supported. **Codex uses `$adaptive-agent-orchestrator`** instead.

**Approval gate:** `Execute based on` begins strategy review, **not immediate implementation**. The Lead must present the execution strategy and wait for explicit approval before executing or spawning execution Workers.

## 8. Safety and compatibility

- A Skill is a policy and workflow bundle; it does not supply native Subagent orchestration or operating-system sandboxing.
- Model and effort settings are platform-specific; Luna/Max is an example preference, not a cross-platform guarantee.
- Permission isolation and independent verification require supported runtime tools.
- Skill structure validation does not establish successful end-to-end execution on your particular agent installation.

Official docs: [Codex](https://developers.openai.com/codex/skills) · [Claude Code](https://code.claude.com/docs/en/skills) · [Antigravity](https://www.antigravity.google/docs/skills)
