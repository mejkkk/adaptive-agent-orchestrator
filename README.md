# Adaptive Agent Orchestrator

**Version 1.1 — Released** · [ภาษาไทย](README.th.md)

A reusable orchestration-policy Skill for **Codex, Claude Code, and Antigravity**. Given existing requirements and an implementation plan, the Lead selects **SOLO (0 Workers)** or **DELEGATED (1+ Workers)**; multi-agent and parallel work are execution styles within DELEGATED. It proposes the execution strategy and **waits for explicit user approval** before implementation.

## How it works

1. **Intake & Review** — Read requirements, implementation plan, and user overrides. Ask only about unresolved critical gaps.
2. **Strategy & Approval** — Break down tasks and dependencies; propose Initial and Maximum Workers, initial Worker roles/models/effort and a concise approach; perform necessary risk and resource checks internally. Wait for approval.
3. **Execution** — Lead may move from SOLO to DELEGATED inside an approved positive Maximum. After delegation Lead never returns to implementation. Add Workers only as justified and notify users.
4. **Verification & Escalation** — Lead reads the reports, checks acceptance criteria, and directly verifies at least one meaningful critical condition. Allow one correction by the original executor, then optionally one attempt by a fresh specialist or stronger model when justified and authorized.
5. **Final Report** — Report artifacts, evidence, cumulative Worker usage/scaling, verification, retry history, blockers and risks.

The Skill stores **orchestration policy only**. Project requirements and implementation plans remain external.

## Documentation

| Document | Purpose |
|---|---|
| [Change history](CHANGELOG.md) | v1.1 changes and earlier history |
| [Workflow (English)](docs/ADAPTIVE_AGENT_ORCHESTRATOR_WORKFLOW_EN.md) | Complete five-phase operational workflow with Mermaid diagrams |
| [Workflow (ภาษาไทย)](docs/ADAPTIVE_AGENT_ORCHESTRATOR_WORKFLOW.md) | Complete Thai-language version with the same Mermaid diagrams |
| [Installation (English)](INSTALLATION.md) | Clone, pull, install, verify and invoke |
| [การติดตั้ง (ภาษาไทย)](INSTALLATION.th.md) | Thai installation guide |
| [Skill entrypoint](skill/adaptive-agent-orchestrator/SKILL.md) | Authoritative English-language Skill policy |
| [Agent metadata](skill/adaptive-agent-orchestrator/agents/openai.yaml) | Display/configuration metadata |
| [Worker contract](skill/adaptive-agent-orchestrator/references/execution-contracts.md) | Worker task/output boundaries |
| [Strategy and approval](skill/adaptive-agent-orchestrator/references/strategy-and-approval.md) | Execution choice and mandatory approval |
| [Verification and escalation](skill/adaptive-agent-orchestrator/references/verification-and-escalation.md) | Direct check and bounded retries |

## Quick start

Clone the repository, then copy the Skill folder into your target project's supported Skill directory:

```bash
git clone https://github.com/mejkkk/adaptive-agent-orchestrator.git
mkdir -p /path/to/project/.agents/skills
cp -R adaptive-agent-orchestrator/skill/adaptive-agent-orchestrator /path/to/project/.agents/skills/
```

Use `.claude/skills/` for Claude Code. See [INSTALLATION.md](INSTALLATION.md) for Windows commands, global installation, updates using `git pull`, and detailed platform paths.

## Prompt examples

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

## Runtime limits

This Skill encodes behavior. Actual agent delegation, sandbox/permission isolation, model availability, and effort settings depend on the host application. A prompt alone cannot guarantee enforcement. Never report unsupported or unverified capabilities as enabled.

## Scope and maintenance

Keep all task-specific requirements outside `skill/adaptive-agent-orchestrator/`. v1.1 updates core policy as well as documentation. Record subsequent behavior changes in [CHANGELOG.md](CHANGELOG.md).
