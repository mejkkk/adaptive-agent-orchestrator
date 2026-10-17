# Adaptive Agent Orchestrator

**Version 1.0 — Released** · [ภาษาไทย](README.th.md)

A reusable orchestration-policy Skill for **Codex, Claude Code, and Antigravity**. Given existing requirements and an implementation plan, the Lead evaluates whether to execute **SOLO**, delegate to **one Worker**, or coordinate **multiple Workers**. It proposes the execution strategy and **waits for explicit user approval** before implementation.

## How it works

1. **Intake & Review** — Read requirements, implementation plan, and user overrides. Ask only about unresolved critical gaps.
2. **Strategy & Approval** — Break down tasks and dependencies; recommend SOLO, DELEGATED, or MULTI-AGENT; specify roles, models, effort, permissions, critical checks, and cost/resource limits. Wait for approval.
3. **Execution** — In SOLO, Lead implements. In delegated modes, Lead coordinates and reviews while Workers implement within explicit task contracts. Parallelize only independent work.
4. **Verification & Escalation** — Lead reads the reports, checks acceptance criteria, and directly verifies at least one meaningful critical condition. Allow one correction by the original executor, then optionally one attempt by a fresh specialist or stronger model when justified and authorized.
5. **Final Report** — Report actual artifacts, evidence, verification results, retry history, blockers, and remaining risks.

The Skill stores **orchestration policy only**. Project requirements and implementation plans remain external.

## Documentation

| Document | Purpose |
|---|---|
| [Workflow](docs/ADAPTIVE_AGENT_ORCHESTRATOR_WORKFLOW.md) | Complete five-phase operational workflow with Mermaid diagrams (Thai) |
| [Workflow source-format text](docs/ADAPTIVE_AGENT_ORCHESTRATOR_WORKFLOW_ORIGINAL.txt) | Companion source-format copy of the same released workflow |
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

**Codex invocation**

```text
$adaptive-agent-orchestrator

Requirements: requirements.md
Implementation Plan: implementation-plan.md
Model preference: Luna, Max Effort
```

**Claude Code / Antigravity invocation (where supported)**: `/adaptive-agent-orchestrator`

The first output is an **Execution Strategy Proposal**, not immediate implementation. Approve that proposal explicitly to start.

## Runtime limits

This Skill encodes behavior. Actual agent delegation, sandbox/permission isolation, model availability, and effort settings depend on the host application. A prompt alone cannot guarantee enforcement. Never report unsupported or unverified capabilities as enabled.

## Scope and maintenance

Keep all task-specific requirements outside `skill/adaptive-agent-orchestrator/`. The Skill and its English-language policy references are intentionally unchanged by documentation-only updates.
