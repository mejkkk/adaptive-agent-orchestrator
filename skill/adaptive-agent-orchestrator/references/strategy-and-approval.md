# Strategy selection and user approval (normative)

## Purpose

Select the smallest credible execution approach for an already scoped task. Require user approval of a clear execution boundary before implementing, then permit reasonable adaptation within that approved boundary.

## Execution modes

- `SOLO`: **0 Workers**; Lead implements and verifies.
- `DELEGATED`: **1+ Workers**; Workers implement; Lead plans, coordinates, reviews and directly inspects evidence. Multi-Agent (2+ Workers) and parallel execution are **styles** of DELEGATED, not separate modes.
- **One-way delegation:** After any Worker is assigned implementation, Lead must not resume implementation in this execution, even if all Workers have finished, failed or become inactive.
- A SOLO execution may transition to DELEGATED without another approval only if its **approved Maximum Workers is positive**, cumulative capacity remains, the work is beneficial and native delegation is available. With Maximum = 0, obtain new approval first.

## Evaluation

1. **Feasibility:** Check source requirements/plan, native Worker tools, permissions and runtime model/effort availability. Do not pretend unsupported settings are active.
2. **Dependencies:** Break down work, identify independent tasks, file conflicts, critical path and integration owner.
3. **Benefit:** Compare specialization, independent verification, context separation and parallel opportunities against coordination, risk and cost.
4. **Initial Workers:** Propose the smallest number actually needed at start, including zero for appropriate SOLO tasks.
5. **Maximum Workers:** Determine a defensible cumulative ceiling from initial demand plus **specific plausible future work**, specialist needs, replacements or conditional fresh-worker escalation. Avoid arbitrary large buffers.
6. **Model/Effort:** Distinguish preferences from hard requirements, verify availability per Worker and mark unknown actual settings `UNVERIFIED`.
7. **Safety:** Internally plan allowed files/actions, shared ownership, critical verification, bounded retries, budget/resource and separate high-risk approval requirements.

## Worker Capacity Planning

- **Initial Workers**: number of Worker instances planned at execution start; integer `>= 0`.
- **Maximum Approved Workers**: total **distinct Worker instances created cumulatively in one execution**, including additional, replacement, verification and fresh escalation Workers. Must be `>= Initial Workers`. Each newly spawned instance consumes one slot permanently, even after it finishes. Reusing that same instance consumes no new slot.
- `Initial = 0, Maximum = 0` is a valid SOLO-only proposal. `Initial = 0, Maximum > 0` allows SOLO initially and preauthorizes a justified one-way transition later.
- **Soft guardrail: five Workers.** Prefer small task-justified ceilings. **Maximum > 5 requires a concrete explanation** of workstreams/contingencies and why fewer Workers are inadequate. Five is neither a hard limit nor the default value to request for every task.
- Maximum is an **authorization ceiling**, not a Worker allocation target. Never pad Maximum merely to avoid later user approval or spawn extra Workers because capacity remains.
- Do not display a separate **Maximum Concurrent Workers** in the ordinary proposal. Actual concurrent use must obey runtime constraints, cumulative cap, dependencies and permission/file-safety boundaries; no unlimited parallelism is implied.

## Required Execution Strategy Proposal (user-facing)

Present a **concise** approval proposal containing:

1. **Task / Source:** short objective and referenced requirements or implementation plan.
2. **Initial Workers / Maximum Workers:** both numbers, and short rationale for Maximum (specific detail mandatory above five).
3. **Initial Worker Configuration:** role, requested model and effort for **each initial Worker**, when Initial > 0. For Initial = 0 show `None`. Clearly mark unverified settings.
4. **Execution Approach:** brief division of work, integration and Lead verification, plus any material risk/runtime capability issue that matters for approval.
5. **User decision:** `Approve`, `Request Changes`, or `Cancel`.

Do **not** routinely display separate fields for Initial Mode, Allowed Modes, Dynamic Scaling, Maximum Concurrency, generic Resource Budget or detailed Task Contracts. Mode follows Worker count and scaling follows this standing policy. This is a presentation rule, **not** permission to omit internal safety checks or conceal material risks or non-standard constraints.

The Lead must internally retain task breakdown and dependencies, role/file ownership, permission boundaries, acceptance criteria, direct Lead critical checks, retry and escalation ceilings, production/high-risk gates, and any applicable budgets or runtime limits.

## Dynamic Worker Scaling

- After strategy approval, the Lead may add Workers **without a new user-approval pause** when the cumulative created count stays `<= Maximum Approved Workers` and scope, task, model hard constraints, permissions, resource and risk boundaries are unchanged.
- Any specialist role must remain inside approved task/responsibility and least-privilege boundaries. A newly risky role or permissions increase needs explicit re-approval even if under Maximum.
- Scale only for justified unfinished work, useful independent checks, specialization or recoveries. Verify task independence, available runtime capacity and integration safety first. Do not scale just because spare slots exist.
- Notify the user for each newly created Worker: instance number, role, requested or confirmed model, effort (or `UNVERIFIED`), reason and **cumulative count / Maximum**. Within the approved envelope this notice is informational, not another approval gate; if real-time notices cannot be emitted, record it in the next progress or final report.
- Reusing a Worker instance does not consume another slot. Ending a Worker never resets the cumulative count. Record scaling rationale for handoff.
- **SOLO → DELEGATED** is authorized when Maximum > 0, new capacity remains and delegation is beneficial/feasible. The transition is **one-way**: after delegating implementation, Lead must not return to code/config changes, state-changing tests, deployment or other implementation.
- When Maximum or runtime capacity is exhausted, do not create a Worker. Replan with existing Workers when safe or ask for a revised approval. Do not silently move delegated implementation back to Lead.

## Authorization state machine

`PREPARING` → `PROPOSED` → `APPROVED` → `EXECUTING` → `VERIFYING` → `COMPLETE | PARTIAL | BLOCKED | FAILED`

- Implementation, mutating tests and execution-Worker creation require explicit approval of the current strategy. Requests to revise are not approval.
- Scaling or SOLO → DELEGATED **inside** the approved cumulative ceiling and boundaries needs no further approval. Increases beyond any approved ceiling, permission/role-risk expansion, scope changes and resource overages require re-approval.
- Production deployment, destructive operations, credential access, new external access or similarly high-impact operations still require their own explicit authorization; approval of ordinary code execution is not standing approval for them.
- If real native Workers are unavailable, disclose it; never pretend separate agents exist. Offer a revised safe strategy or stop. If the execution has already delegated, Lead must not implement as fallback.

## Preferences and hard constraints

- "Prefer Luna at Max Effort" is a preference, subject to real availability and role fit.
- "Use only Luna" is a hard constraint. If unsupported, ask rather than silently substitute.
- "Use 3 Workers" is input for evaluation; explain a smaller/better plan when justified and obtain approval.
- Treat unverifiable actual model/effort settings as `UNVERIFIED`, never as confirmed.
