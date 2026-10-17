# Verification, bounded retry, and escalation (normative)

## Initial review: mandatory in every mode

The Lead must:

1. Read the original implementer's report and referenced evidence, including failures and unverified statements.
2. Compare actual deliverables against the user's requirements, approved implementation plan, and **all required acceptance criteria**.
3. Make **at least one direct check of a meaningful critical criterion on a real artifact or system** using authorized read-only inspection where possible; capture exactly what was checked and the observed result. Examples: inspect the real output produced from a test input; read a configuration value; inspect a file or live service status; invoke a truly non-mutating tool that validates a real response.
4. For high-risk work, require verification of *every applicable critical/safety criterion* and appropriate independent test evidence. One direct check is only a minimum, never a blanket sign-off.
5. If direct Lead inspection is technically unavailable, report `LEAD DIRECT CHECK: NOT VERIFIED`, delegate independent verification when supported and approved, and explain the effect on acceptance. Never represent a Worker's report as the Lead's own check.

Do not run production-altering, state-changing, or privilege-escalating checks directly as Lead after delegation, including when no Workers remain active. Delegate with appropriate authorization. Testing may create output or change state; classify it before attempting.

## Per-root-cause retry state machine

`INITIAL FAIL → DIAGNOSE → ORIGINAL CORRECTION (max 1) → REVERIFY → OPTIONAL FRESH WORKER CORRECTION (max 1) → REVERIFY → ACCEPT or STOP/USER DECISION`

### Diagnose before retry

- Identify which acceptance criterion failed, observable symptoms, error output, likely root cause, prior steps, and objective evidence.
- If blocked by missing permissions, credentials, environments, external dependencies, missing user decisions, or unsupported runtime behavior with no authorized remedy: **stop early** and ask the user for a decision. Don't consume attempts by changing model.
- Do not repair outside approved scope; do not restart the counter by renaming a symptom.

### Attempt 1: original executor

- If fixable: give the **same original Worker** (delegated modes), or Lead (SOLO), a precise failure report and allow **one correction attempt**.
- Reverify the relevant failed criterion and affected regressions. If it passes all mandatory criteria, accept; otherwise determine whether fresh-worker escalation could reasonably help.

### Attempt 2: optional new specialist

- Only if the failed criterion persists and a *distinct* specialist, independent approach, or more capable model is likely to address the actual cause: propose/spawn a **fresh Worker**, authorized for a **single correction attempt**.
- Prefer a better-suited role/model/effort that exists in the actual platform; don't claim an unavailable "higher" level. Give the new Worker the approved task scope, reproducible failure evidence, and an independent diagnosis brief. Avoid having it blindly repeat the same patch.
- Count each fresh correction Worker against the **cumulative Maximum Approved Workers**, including Workers replacing inactive ones. Respect model/effort hard constraints, permissions, scope, resource limits and real runtime capabilities. If capacity is exhausted or any boundary is exceeded, request approval **before spawning**.
- In approved SOLO, **Maximum Workers > 0** preauthorizes a justified fresh-Worker correction within the envelope; with Maximum = 0, obtain revised approval first. Once this Worker is delegated, Lead never resumes implementation for the current execution.
- After the one attempt, Lead reverifies. If still failing, **stop and report to user**; no third automatic attempt for the same root cause.
- If a fresh Worker is clearly unhelpful, prohibited, impossible, or disproportionately expensive, skip it and escalate to the user directly.

### Related or new issues

- Track retry count per underlying root cause rather than per text message or filename. Do not use a "new bug" label to bypass a stuck root cause.
- Independent newly discovered problems may be tracked separately **within the approved overall resource budget**; ask for user direction if the project turns into an open-ended cascade.
- If a completed fix introduces a safety-critical regression, stop risky operations and seek a decision before further changes beyond the approved strategy.

## Final verification outcome

| Outcome | Required evidence | Action |
| --- | --- | --- |
| `PASS` | Required criteria met; direct check documented as actually performed | Accept and move to final report |
| `FAIL` | Specific failed criterion and evidence | Fix within remaining authorized attempts, or stop |
| `NOT VERIFIED` | Check could not be performed or evidence missing | Report uncertainty; do not claim fully complete |
| `BLOCKED` | Missing external authority/dependency or runtime capability | Stop and request user decision |

The final report must include original failure, corrections, actual checks and results, all retry counts, remaining risks, and what specific choice the user should make if unresolved. Avoid confident statements unsupported by observed results.