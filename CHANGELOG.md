# Changelog

This file records meaningful changes to **Adaptive Agent Orchestrator**. Consult the [GitHub commit history](https://github.com/mejkkk/adaptive-agent-orchestrator/commits/main/) for detailed file diffs and timestamps.

## [1.1.0] — 2026-10-17

### Changed
- Consolidated three former execution labels into **two modes**: SOLO (0 Workers) and DELEGATED (1+ Workers). Multi-Agent and Parallel are execution styles under DELEGATED.
- Added **one-way SOLO → DELEGATED** within a pre-approved positive Maximum; Lead must not return to implementation after any implementation delegation.
- Defined **Initial Workers** and **Maximum Approved Workers** as a cumulative total of distinct Worker instances created during an execution, including replacements, verification Workers and fresh escalation Workers.
- Introduced a **soft planning guardrail of five Workers**. Proposals above five require task-specific reasons; five is not a hard maximum or a default allocation.
- Enabled Worker Scaling without repeated approval inside the authorized scope, cumulative Maximum, role, permission, risk and resource boundaries. Additional Worker creation is reported with role, model, effort, reason and running count.
- Simplified user-facing **Execution Strategy Approval** to task/source, Initial/Maximum, initial Worker configuration, brief approach and an explicit approval decision. Internal checks still apply.
- Removed the routine Maximum Concurrent Workers field; actual parallelism depends on runtime capacity and safe dependencies within the cumulative Maximum.
- Updated core SKILL.md and all three policy references, both Mermaid-enabled Workflow documents, English/Thai README and Installation guides, and AGENTS.md.

### Preserved
- Explicit invocation and mandatory **human approval before implementation**.
- Strict Lead/Worker separation, direct Lead critical verification and evidence-based reporting.
- One original-executor correction and one conditional fresh-worker correction per underlying root cause.
- Separate approval requirements for production operations, expanded permissions and other high-risk work.

## [1.0.0] — Prior release

- Established the five phases: Intake & Review; Strategy & Approval; Execution; Verification & Escalation; Final Report & Handoff.
- Published the reusable Skill, OpenAI metadata, reference policies, bilingual workflow documents and installation guidance for Codex, Claude Code and Antigravity.
- Subsequent v1.0 documentation changes added concise prompts with and without optional overrides.
