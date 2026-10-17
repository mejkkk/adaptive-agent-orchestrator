# Strategy selection and user approval (normative)

## Purpose

Select the simplest credible execution approach for the already scoped task. The user decides whether to proceed after seeing an explicit strategy. Avoid assuming that a long plan always needs many agents.

## Evaluate in this order

1. **Feasibility:** Can the current session safely accomplish the task with available permissions, tools, context, and budget? Identify missing runtime capabilities. An unusable role/model cannot be treated as available.
2. **Dependencies:** Are subtasks independent, or will Workers spend most of their time waiting on shared files and decisions?
3. **Value of delegation:** Assess specialist expertise, isolation of context, independent review, likely elapsed-time reduction, quality/risk benefits, and costs of coordinating/merging.
4. **Choose mode:**
   - `SOLO`: Direct implementation is simpler and no clear benefit from delegation.
   - `DELEGATED`: One specialist or one independent executor offers a meaningful benefit while Lead focuses on oversight/review.
   - `MULTI_AGENT`: Two or more workers offer distinct roles or safely parallelizable tasks with measurable upside.
5. **Cap size:** Propose initial count and maximum authorized concurrent or total Workers separately. A task with 10 sequential steps does not imply 10 Workers. Include a shared-file integration strategy.
6. **Model/Effort:** Start with user preference (e.g., Luna with Max Effort), check actual availability and suitability by role, then propose precise alternatives with reasons. Treat wording like "prefer" as negotiable and "only" as a hard limit. State unknown actual values as `UNVERIFIED` rather than guessing. A stronger label does not guarantee a better result.
7. **Safety:** Define which actions are read-only, mutating, remote, sensitive, destructive or production-facing, and when new user approval is mandatory.

## Required Execution Strategy Proposal

Before implementation or execution-worker creation, present at least:

- **Proposal ID or revision**, summarized goal and accepted source requirements/plan (include unresolved assumptions).
- **Recommendation + rationale:** `SOLO`, `DELEGATED`, or `MULTI_AGENT`; why this mode beats plausible alternatives given cost/time/quality/risk. For SOLO explicitly say no Subagent is needed. If a single Worker is better, recommend one.
- **Task breakdown/dependency graph**: tasks, owner, dependencies, critical path, safe parallel opportunities, planned sequence.
- **Worker matrix** (if any): role, specific responsibility, initial instance count, model, effort, availability/actual-verification status, tools, file ownership, allowed operations, and output checks.
- **Execution envelope:** initial and maximum authorized Workers, max concurrency, reasonable time/token/cost budget if known (otherwise label `NOT SET`), platform and permission limitations.
- **Lead verification:** at least one exact critical check on the real outcome, what access is required, what will be delegated if Lead cannot perform it; additional critical checks for high-risk work.
- **Failure policy:** original executor's one correction, optional new-worker one correction, triggers that stop early, preauthorization (or lack thereof) for a SOLO-to-WORKER fallback or other escalation.
- **User approval question:** explicitly request `Approve`, `Request changes`, or `Cancel`. Do not start work while waiting.

If a user asks for different roles, models, worker counts, parallelism, or budgets, examine whether they are safe and useful; explain objections and tradeoffs rather than obeying blindly. An updated recommendation requires an updated approval.

## Authorization state machine

`PREPARING` → `PROPOSED` → `APPROVED` → `EXECUTING` → `VERIFYING` → `COMPLETE | PARTIAL | BLOCKED | FAILED`

- `PROPOSED` may go back to `PREPARING` when the user requests changes.
- `APPROVED` is reached only after explicit user confirmation referencing the currently proposed strategy. Invoking the skill or asking "start" before seeing a proposal does **not** skip this gate.
- When execution needs scope, model hard-constraint, permission, worker ceiling, budget, or risky-operation changes, pause at a **new proposal/approval** gate; do not quietly mutate the approved plan.
- Approval to execute ordinary code is not standing approval for production deployment, deletion, credential access or similarly high-impact actions.
- If real native subagents are unavailable, do not mimic them. Explain and propose a revised SOLO strategy for approval or stop.

## Preference versus hard constraint

- "Prefer Luna at Max Effort for workers" → use it as the first candidate; offer different settings by role when justified and supported.
- "Use only Luna; do not change models" → hard constraint; if unsupported, ask for a new decision rather than switch without permission.
- "Use 3 Workers" → interpret as a user request. If that is inefficient or conflicts with safe concurrency, explain why and propose 1–2 or SOLO. Wait for approval.
- If a model or effort cannot be verified by the runtime, say so. Do not claim a configuration was applied just because it was included in the task prompt.