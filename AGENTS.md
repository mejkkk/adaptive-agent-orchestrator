# Repository agent instructions

- This repository packages the `adaptive-agent-orchestrator` policy Skill. The active entrypoint is `skill/adaptive-agent-orchestrator/SKILL.md`.
- Treat `docs/FULL_WORKFLOW_FINAL_DESIGN_REVIEW_ORIGINAL.txt` as an immutable record of the approved original review. Do not rewrite its content or replace historical references when preparing changes.
- Keep task-specific requirements and implementation plans outside the reusable Skill.
- When editing the Skill, preserve explicit user approval before execution, SOLO/delegated mode selection, strict Lead/Worker execution boundaries, direct Lead verification, the one-original-attempt plus conditional one-fresh-worker retry limit, and evidence-based final reporting.
- Do not claim runtime-enforced permission isolation or support for a particular model/effort without checking the actual platform.