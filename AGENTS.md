# Repository agent instructions

- This repository publishes the **Adaptive Agent Orchestrator v1.1** policy Skill. The active entrypoint is `skill/adaptive-agent-orchestrator/SKILL.md`.
- The released workflow is maintained in `docs/ADAPTIVE_AGENT_ORCHESTRATOR_WORKFLOW_EN.md` (English) and `docs/ADAPTIVE_AGENT_ORCHESTRATOR_WORKFLOW.md` (Thai). Keep both aligned, preserving five phases, Mermaid diagrams, execution semantics and critical policies.
- Maintain English as the primary documentation language for `README.md` and `INSTALLATION.md`, with matching Thai companions `README.th.md` and `INSTALLATION.th.md`.
- Do not add task-specific requirements or implementation plans to the reusable Skill.
- Preserve two execution modes: SOLO (0 Workers) and DELEGATED (1+ Workers). Multi-Agent and parallel execution are styles inside DELEGATED.
- Preserve explicit initial approval; support one-way SOLO → DELEGATED inside a positive approved Maximum. Lead must not return to implementation after delegation.
- Maximum Workers is cumulative across created instances, including replacements and escalation. Use five as a soft guardrail requiring justification above five, not a fixed cap.
- Permit justified scaling inside the envelope with user notification, while preserving safe Lead/Worker boundaries, direct checks, one original correction, one conditional fresh-worker correction and evidence-based reporting.
- Do not claim runtime-enforced permission isolation or actual Model/Effort support without checking the current platform.
- Update [CHANGELOG.md](CHANGELOG.md) when releasing new Skill behavior and keep English/Thai documents in sync.
