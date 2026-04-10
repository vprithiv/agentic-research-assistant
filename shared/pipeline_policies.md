# Pipeline Policies — Single Source of Truth

All pipeline agents MUST defer to this file for policy decisions. If any other file contradicts a policy here, this file wins.

---

## P1: Integrity Gate Rules

### Skip rules
- **Stage 4.5**: NEVER skippable. Always runs full Mode 2 verification, regardless of passport status.
- **Stage 2.5**: Mandatory by default. Can only be reduced or skipped when ALL three conditions are met:
  1. User provides a valid Material Passport
  2. Content has NOT been modified since verification (compare `version_label`)
  3. User explicitly chooses from: (a) skip, (b) spot-check *(recommended default)*, (c) full
- The orchestrator MUST NOT auto-skip Stage 2.5 even if the passport is valid.

### PASS requirement
- Both Stage 2.5 and 4.5 must achieve PASS or PASS_WITH_NOTES to proceed to their next stage.
- Stage 2.5 PASS or PASS_WITH_NOTES required before Stage 3 (REVIEW).
- Stage 4.5 PASS or PASS_WITH_NOTES required before Stage 5 (FINALIZE).
- PASS = zero CRITICAL, SERIOUS, or MEDIUM issues. PASS_WITH_NOTES = zero CRITICAL/SERIOUS/MEDIUM but has MINOR issues or UNVERIFIABLE_ACCESS flags (advisory, does NOT block pipeline). FAIL = any CRITICAL, SERIOUS, or MEDIUM issue present. Note: UNVERIFIABLE_ACCESS is a tool-limitation flag (paywall), not a severity level — it never blocks the pipeline.

### Stage 4.5 independence
- Stage 4.5 is a FRESH full verification of ALL references, independent of Stage 2.5.
- It must verify every reference as if Stage 2.5 never happened (Stage 2.5 may have had sampling gaps).
- Comparing with Stage 2.5 results is supplementary, not a replacement.

---

## P2: Integrity Failure Handling

### Correction loop
On FAIL verdict (either Stage 2.5 or 4.5):
1. Produce correction list sorted by severity
2. Fix items (use WebSearch to confirm correct information)
3. Re-verify only corrected items
4. If all pass → PASS
5. If issues remain → repeat (max **3 rounds** total)

### After 3 failed rounds
- List all unverifiable items for the user
- User must **resolve or remove** every item before proceeding — cannot bypass integrity gate
- If user cannot resolve: pipeline aborts with a detailed report

### Stage 2.5 FAIL routing
- Corrections happen in-place at Stage 2.5 (re-verify loop above)
- If corrections require substantial rewriting, the orchestrator routes back to Stage 2 (WRITE) with integrity issues as revision requirements

### Stage 4.5 FAIL routing
- Return to Stage 4' (RE-REVISE) with integrity issues
- After revision, re-run Stage 4.5 (counts toward the 3-round limit)

---

## P3: Checkpoint Policy

- **Every stage completion** requires user confirmation before proceeding to the next stage.
- Checkpoint types:
  - **GATE**: Integrity boundaries (2.5, 4.5), review decisions (3, 3', 3.5), before finalization (5). Cannot be skipped.
  - **NOTIFY**: All other transitions. Auto-proceed after user confirmation.

---

## P4: Review-Only Routing

- User says "review my paper" (without mentioning check/verify/pipeline) → route to `peer-review` standalone. No pipeline, no integrity check.
- User says "check and review" / "verify and review" / "full pipeline" → enter pipeline at Stage 2.5, then Stage 3.
- User says "check" / "verify citations" (without "review") → Stage 2.5 only.

---

## P5: Gray-Zone Verdicts Prohibited

- Every reference must reach a terminal verdict. Allowed verdicts:
  - **VERIFIED**: DOI resolves + metadata matches
  - **NOT_FOUND**: 3 search attempts failed → suspected fabrication
  - **MISMATCH**: Source exists but metadata differs (wrong year, wrong authors, etc.)
  - **MANUAL_CHECK_REQUIRED**: Vague reference with no title and no DOI — cannot be automatically verified. Flagged for human resolution.
  - **BOOK_NOT_VERIFIED**: Book (ISBN or publisher known) — skipped automated verification. Flagged for human confirmation.
- "Difficult to verify" is NOT a verdict. After 3 search attempts with different queries → classify as NOT_FOUND (suspected fabrication).
- "Partially verified" or "plausible but unconfirmed" buckets are prohibited.
- MANUAL_CHECK_REQUIRED and BOOK_NOT_VERIFIED do not block the pipeline but MUST be listed in the integrity report for user review.

---

## P6: Skippable vs Non-Skippable Stages

| Skippable (with warning) | Non-Skippable |
|--------------------------|---------------|
| Stage 1 (if user provides own bibliography) | Stage 2 (writing) |
| Stage 3' (if only minor revisions) | Stage 2.5 (see P1 for passport exception) |
| Stage 4' (if accepted at re-review) | Stage 3 (initial review) |
| | Stage 4.5 (always full, never skippable) |
| | Stage 5 (finalize) |

---

## P7: Audit Trail

- All passport check decisions (skip/spot-check/full) must be logged in `state_tracker` for the pipeline audit trail.
- All integrity verdicts and correction rounds must be recorded.

---

## P8: Model Routing Policy

### Default tiers are advisory

- Each agent in `agent_registry.md` has a default Model tier (opus, sonnet, or haiku).
- These defaults are **recommendations**, not hard constraints. The user can override any agent's model at any time.

### Override rules

- **User override**: The user may specify a different model for any agent. The pipeline must respect this without warning or resistance.
- **Escalation**: If a Sonnet-tier agent produces inadequate output (malformed, shallow reasoning, missing key analysis), the pipeline may escalate that agent to Opus. Escalation applies to **that agent only** — do not upgrade the entire pipeline.
- **Never silently upgrade to Opus.** Before escalating, log the reason and notify the user at the next checkpoint.
- **Downgrades** are permitted when the task is simpler than expected (e.g., `formatter_agent` on plain Markdown stays at Haiku).

### Logging

- All model overrides and escalations must be recorded in the stage manifest:
  ```json
  {
    "model_overrides": [
      {"agent": "formatter_agent", "default": "sonnet", "actual": "haiku", "reason": "Plain Markdown output, no LaTeX needed"}
    ]
  }
  ```
- The `state_tracker_agent` includes model tier in its checkpoint records.

### Cost reporting

- At pipeline start, the orchestrator reports the estimated cost distribution to the user based on default model tiers.
- At pipeline end, the orchestrator reports actual model usage vs. defaults, including any escalations.

### Automated escalation triggers

In addition to manual escalation, the following conditions trigger automatic escalation consideration:
- **Schema validation failure**: If a Sonnet/Haiku agent's output fails handoff schema validation (missing required fields, wrong types), escalate to the next tier and retry.
- **Output length anomaly**: If a Sonnet agent produces output < 30% of the expected length for its task type (suggesting shallow output), flag for escalation review.
- **Downstream rejection**: If a consuming agent returns `HANDOFF_INCOMPLETE` for a Sonnet agent's output, escalate the producing agent to Opus for retry.
- All automated escalations are logged in the stage manifest and reported at the next checkpoint.
