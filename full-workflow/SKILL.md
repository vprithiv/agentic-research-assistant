---
name: full-workflow
description: "Orchestrator for the full academic research pipeline: research -> write -> integrity check -> review -> human review gate -> revise -> re-review -> re-revise -> final integrity check -> finalize -> process summary. Coordinates literature-review, paper-writing, and peer-review into an 11-stage workflow with systematic integrity verification, two-stage structured self-review, and reproducible quality gates. Triggers on: academic pipeline, research to paper, full paper workflow, paper pipeline, end-to-end paper, research-to-publication, complete paper workflow."
metadata:
  version: "3.0"
  last_updated: "2026-04-07"
  depends_on: "literature-review, paper-writing, peer-review"
---

# Academic Pipeline v3.0 — Full Academic Research Workflow Orchestrator

A lightweight orchestrator that manages the complete academic pipeline from research exploration to final manuscript. It does not perform substantive work — it only detects stages, recommends modes, dispatches skills, manages transitions, and tracks state.

**v2.0 Core Improvements**:
1. **Mandatory user confirmation checkpoints** — Each stage completion requires user confirmation before proceeding to the next step
2. **Academic integrity verification** — After paper completion and before review submission, systematic reference spot-checking and data verification must pass
3. **Two-stage review** — First full review + post-revision focused verification review
4. **Final integrity check** — After revision completion, re-verify all citations and data (within automated verification capabilities)
5. **Reproducible** — Standardized workflow producing consistent quality assurance each time
6. **Process documentation** — After pipeline completion, automatically generates a "Paper Creation Process Record" PDF documenting the human-AI collaboration history

## Capability Boundaries (Read Before Using)

This pipeline coordinates AI-assisted academic work. Before starting, understand what it CAN and CANNOT do:

| Capability | Status | Details |
|-----------|--------|---------|
| Literature search | PARTIAL | Searches via WebSearch; cannot access most paywalled databases directly. Coverage is incomplete. |
| Reference verification | METADATA ONLY | Confirms DOIs resolve and bibliographic data matches. Does NOT verify cited findings are correctly interpreted. |
| Statistical analysis | CANNOT DO | Can plan analyses and interpret results you provide. Cannot execute computations on raw data. |
| Peer review | SELF-CHECK ONLY | Structured quality assessment from AI perspectives. Not a substitute for independent human review. |
| Originality assessment | APPROXIMATE | Can flag obvious overlaps via WebSearch. Not a plagiarism detection tool (use Turnitin/iThenticate). |
| Writing quality | GOOD | Can produce well-structured academic prose. |
| Citation formatting | GOOD | Reliable for APA 7, Chicago, MLA, IEEE, Vancouver. |
| Integrity verification | SPOT-CHECK | Systematic but not infallible. Human verification of critical claims recommended. |

**Bottom line**: This pipeline is a powerful drafting and quality-improvement assistant. It is NOT an autonomous paper-production system. The human researcher's domain expertise, original thinking, and judgment remain essential at every stage.

## Quick Start

**Full workflow (from scratch):**
```
I want to write a research paper on the impact of AI on higher education quality assurance
```
--> full-workflow launches, starting from Stage 1 (RESEARCH)

**Mid-entry (existing paper):**
```
I already have a paper, help me review it
```
--> Route to `peer-review` standalone (no pipeline, no integrity check). If user wants the full pipeline with integrity, they should say "full pipeline" or "check and review my paper"

**Revision mode (received reviewer feedback):**
```
I received reviewer comments, help me revise
```
--> full-workflow detects, starting from Stage 4 (REVISE)

**Execution flow:**
1. Detect the user's current stage and available materials
2. Recommend the optimal mode for each stage
3. Dispatch the corresponding skill for each stage
4. **After each stage completion, proactively prompt and wait for user confirmation**
5. Track progress throughout; Pipeline Status Dashboard available at any time

---

## Trigger Conditions

### Trigger Keywords

**English**: academic pipeline, research to paper, full paper workflow, paper pipeline, end-to-end paper, research-to-publication, complete paper workflow

### Non-Trigger Scenarios

| Scenario | Skill to Use |
|----------|-------------|
| Only need to search materials or do a literature review | `literature-review` |
| Only need to write a paper (no research phase needed) | `paper-writing` |
| Only need to review a paper (no integrity check) | `peer-review` (standalone) |
| Only need to check citation format | `paper-writing` (citation-check mode) |
| Only need to convert paper format | `paper-writing` (format-convert mode) |

### Trigger Exclusions

- If the user only needs a single function (just search materials, just check citations), no pipeline is needed — directly trigger the corresponding skill
- If the user is already using a specific mode of a skill, do not force them into the pipeline
- The pipeline is optional, not mandatory

---

## Pipeline Stages (11 Stages)

| Stage | Name | Skill / Agent Called | Available Modes | Deliverables |
|-------|------|---------------------|----------------|-------------|
| 1 | RESEARCH | `literature-review` | socratic, full, quick | RQ Brief, Methodology, Bibliography, Synthesis |
| 2 | WRITE | `paper-writing` | plan, full | Paper Draft |
| **2.5** | **INTEGRITY** | **`integrity_verification_agent`** | **pre-review** | **Integrity verification report + corrected paper** |
| 3 | REVIEW | `peer-review` | full (incl. Devil's Advocate) | 5-perspective analysis reports + Editorial Decision + Revision Roadmap (structured self-review) |
| **3.5** | **HUMAN REVIEW GATE** | **orchestrator** | **mandatory** | **Human review solicitation; state persistence if paused** |
| 4 | REVISE | `paper-writing` | revision | Revised Draft, Response to Reviewers |
| **3'** | **RE-REVIEW** | **`peer-review`** | **re-review** | **Verification review report: revision response checklist + residual issues** |
| **4'** | **RE-REVISE** | **`paper-writing`** | **revision** | **Second revised draft (if needed)** |
| **4.5** | **FINAL INTEGRITY** | **`integrity_verification_agent`** | **final-check** | **Final verification report (must achieve PASS or PASS_WITH_NOTES per P1 to proceed)** |
| 5 | FINALIZE | `paper-writing` | format-convert | Final Paper (default MD + DOCX; ask about LaTeX; confirm correctness; PDF) |
| **6** | **PROCESS SUMMARY** | **orchestrator** | **auto** | **Paper creation process record MD + LaTeX to PDF** |

---

## Pipeline State Machine

1. **Stage 1 RESEARCH** -> user confirmation -> Stage 2
2. **Stage 2 WRITE** -> user confirmation -> Stage 2.5
3. **Stage 2.5 INTEGRITY** -> PASS or PASS_WITH_NOTES -> Stage 3 (FAIL -> fix and re-verify, max 3 rounds)
4. **Stage 3 REVIEW** -> Accept -> Stage 3.5 -> Stage 4.5 / Minor|Major -> Stage 3.5 -> Stage 4 / Reject -> Stage 2 or end
5. **Stage 3.5 HUMAN REVIEW GATE** -> Pause (save state) / Enter human feedback / Continue (AI-only)
6. **Stage 4 REVISE** -> user confirmation -> Stage 3'
7. **Stage 3' RE-REVIEW** -> Accept|Minor -> Stage 4.5 / Major -> Stage 4'
8. **Stage 4' RE-REVISE** -> user confirmation -> Stage 4.5 (no return to review)
9. **Stage 4.5 FINAL INTEGRITY** -> PASS or PASS_WITH_NOTES -> Stage 5 (FAIL -> fix and re-verify)
10. **Stage 5 FINALIZE** -> MD + DOCX -> ask about LaTeX -> confirm -> PDF -> Stage 6
11. **Stage 6 PROCESS SUMMARY** -> ask language version -> generate process record MD -> LaTeX -> PDF -> end

See `references/pipeline_state_machine.md` for complete state transition definitions.

---

## Simplified Checkpoint System

Two types only:

1. **GATE** — Cannot proceed without explicit user input.
   Used at: Stage 1->2, Stage 2.5, Stage 3->3.5, Stage 3.5->4, Stage 4.5, Stage 5

2. **NOTIFY** — Inform user of completion, auto-proceed after confirmation.
   Used at: All other transitions.

Remove: SLIM type, awareness guard, auto-continue counting. These added complexity without proportionate value.

---

## File-Based State Persistence

All pipeline state is persisted to `.pipeline/state.json` in the project directory.

On pipeline start: Create `.pipeline/state.json`
On stage completion: Update stage status, record output files
On stage start: Read state to determine entry point
On conversation resume: Read state to recover position

This enables:
- State survives conversation interruptions
- User can inspect state (`cat .pipeline/state.json`)
- Mid-entry by reading existing state
- Auditable without LLM involvement

---

## Agent Team (3 Agents)

| # | Agent | Role | File |
|---|-------|------|------|
| 1 | `pipeline_orchestrator_agent` | Main orchestrator: detects stage, recommends mode, triggers skill, manages transitions | `agents/pipeline_orchestrator_agent.md` |
| 2 | `state_tracker_agent` | State tracker: records completed stages, produced materials, revision loop count | `agents/state_tracker_agent.md` |
| 3 | `integrity_verification_agent` | Automated integrity spot-check: systematic reference/citation/data verification (within automated verification capabilities) | `agents/integrity_verification_agent.md` |

---

## Orchestrator Workflow

### Step 1: INTAKE & DETECTION

```
pipeline_orchestrator_agent analyzes the user's input:

1. What materials does the user have?
   - No materials           --> Stage 1 (RESEARCH)
   - Has research data      --> Stage 2 (WRITE)
   - Has paper draft        --> Stage 2.5 (INTEGRITY)
   - Has verified paper     --> Stage 3 (REVIEW)
   - Has review comments    --> Stage 4 (REVISE)
   - Has revised draft      --> Stage 3' (RE-REVIEW)
   - Has final draft for formatting --> Stage 5 (FINALIZE)

2. What is the user's goal?
   - Full workflow (research to publication)
   - Partial workflow (only certain stages needed)

3. Determine entry point, confirm with user
```

### Step 2: MODE RECOMMENDATION

```
Based on entry point and user preferences, recommend modes for each stage:

User type determination:
- Novice / wants guidance --> socratic (Stage 1) + plan (Stage 2) + guided (Stage 3)
- Experienced / wants direct output --> full (Stage 1) + full (Stage 2) + full (Stage 3)
- Time-limited --> quick (Stage 1) + full (Stage 2) + quick (Stage 3)

Explain the differences between modes when recommending, letting the user choose
```

### Step 3: STAGE EXECUTION

```
Call the corresponding skill (does not do work itself, purely dispatching):

1. Inform the user which Stage is about to begin
2. Load the corresponding skill's SKILL.md
3. Launch the skill with the recommended mode
4. Monitor stage completion status

After completion:
1. Compile deliverables list
2. Update pipeline state (call state_tracker_agent)
3. [MANDATORY] Proactively prompt checkpoint, wait for user confirmation
```

### Step 4: TRANSITION

```
After user confirmation:

1. Pass the previous stage's deliverables as input to the next stage
2. Trigger handoff protocol (defined in each skill's SKILL.md):
   - Stage 1  --> 2: literature-review handoff (RQ Brief + Bibliography + Synthesis)
   - Stage 2  --> 2.5: Pass complete paper to integrity_verification_agent
   - Stage 2.5 --> 3: Pass verified paper to reviewer
   - Stage 3  --> 4: Pass Revision Roadmap to paper-writing revision mode
   - Stage 4  --> 3': Pass revised draft and Response to Reviewers to reviewer
   - Stage 3' --> 4': Pass new Revision Roadmap to paper-writing revision mode
   - Stage 4/4' --> 4.5: Pass revision-completed paper to integrity_verification_agent (final verification)
   - Stage 4.5 --> 5: Pass verified final draft to format-convert mode
3. Begin next stage
```

---

## Integrity Review Protocol (Added in v2.0)

### Stage 2.5: First Integrity Check (Pre-Review Integrity)

**Trigger**: After Stage 2 (WRITE) completion, before Stage 3 (REVIEW)
**Purpose**: Ensure all references and data are not fabricated or erroneous before submission for review

```
Execution steps:
1. integrity_verification_agent executes Mode 1 (initial verification) on the paper
2. Verification scope:
   - Phase A: 100% reference existence + bibliographic accuracy + ghost citations (within automated verification capabilities)
   - Phase B: >= 30% citation context spot-check
   - Phase C: 100% statistical data verification (within automated verification capabilities)
   - Phase D: >= 30% originality spot-check + self-plagiarism check
   - Phase E: 30% claim verification spot-check (minimum 10 claims)
3. Result handling:
   - PASS or PASS_WITH_NOTES -> checkpoint -> Stage 3
   - FAIL -> produce correction list -> fix item by item -> re-verify corrected items
   - PASS after corrections -> checkpoint -> Stage 3
   - Still FAIL after 3 rounds -> notify user, list unverifiable items
```

### Stage 4.5: Final Integrity Check (Post-Revision Final Check)

**Trigger**: After Stage 4' (RE-REVISE) or Stage 3' (RE-REVIEW, Accept) completion, before Stage 5 (FINALIZE)
**Purpose**: Confirm the revised paper passes systematic reference spot-checking and is ready for publication

```
Execution steps:
1. integrity_verification_agent executes Mode 2 (final verification) on the revised draft
2. Verification scope:
   - Phase A: 100% reference verification (within automated verification capabilities) (including those added during revision)
   - Phase B: 100% citation context verification (within automated verification capabilities) (not spot-check, full check)
   - Phase C: 100% statistical data verification (within automated verification capabilities)
   - Phase D: >= 50% originality spot-check (100% for newly added/modified paragraphs, within automated verification capabilities)
   - Phase E: 100% claim verification (within automated verification capabilities) (zero MAJOR_DISTORTION + zero UNVERIFIABLE required)
3. Special check: Compare with Stage 2.5 results to confirm all previous issues are resolved
4. Result handling:
   - PASS or PASS_WITH_NOTES -> checkpoint -> Stage 5
   - FAIL -> fix -> re-verify -> PASS or PASS_WITH_NOTES -> Stage 5
5. **Must achieve PASS or PASS_WITH_NOTES to proceed to Stage 5 (per P1)**
```

---

## Two-Stage Review Protocol (Added in v2.0)

### Stage 3: First Review (Full Review)

- **Input**: Paper that passed integrity check
- **Review team**: EIC + R1 (methodology) + R2 (domain) + R3 (interdisciplinary) + Devil's Advocate
- **Output**: 5-perspective analysis reports + Editorial Decision + Revision Roadmap + Socratic Revision Coaching
- **Decision branches**: Accept -> Stage 3.5 -> Stage 4.5 / Minor|Major -> Stage 3.5 -> Revision Coaching -> Stage 4 / Reject -> Stage 2 or end

See `peer-review/SKILL.md` for review process details.

### Stage 3.5: HUMAN REVIEW GATE (Mandatory)

After the AI self-review (Stage 3) produces its Revision Roadmap:

1. Display the Revision Roadmap summary
2. Display: "The AI self-review is complete. Before proceeding to revision, we STRONGLY RECOMMEND sharing this paper with a human reviewer (advisor, colleague, domain expert). Their feedback will catch issues the AI review cannot."
3. Ask: "Would you like to:"
   a. **Pause** the pipeline to get human feedback (recommended)
   b. **Enter** human reviewer feedback now (if you already have it)
   c. **Continue** with AI-only review (acknowledge limitation)

If (a): Save state to `.pipeline/state.json`, provide resume instructions.
If (b): Activate External Review Protocol.
If (c): Log "human-review-skipped" in audit trail. Add to final paper: "Note: This paper was reviewed using AI-assisted self-review only. Independent human peer review was not incorporated before this version."

### Stage 3 -> 4 Transition: Revision Coaching

EIC uses Socratic dialogue to guide the user in understanding review comments and planning revision strategy (max 8 rounds). User can say "just fix it for me" to skip.

### Stage 3': Second Review (Verification Review)

- **Input**: Revised draft + Response to Reviewers + original Revision Roadmap
- **Mode**: `peer-review` re-review mode
- **Output**: Revision response comparison table + new issues list + new Editorial Decision
- **Decision branches**: Accept|Minor -> Stage 4.5 / Major -> Residual Coaching -> Stage 4'

See `peer-review/SKILL.md` Re-Review Mode for verification review process.

### Stage 3' -> 4' Transition: Residual Coaching

EIC guides the user in understanding residual issues and making trade-offs (max 5 rounds). User can say "just fix it" to skip.

---

## Mid-Entry Protocol

Users can enter from any stage. The orchestrator will:

1. **Detect materials**: Analyze the content provided by the user to determine what is available
2. **Identify gaps**: Check what prerequisite materials are needed for the target stage
3. **Suggest backfilling**: If critical materials are missing, suggest whether to return to earlier stages
4. **Direct entry**: If materials are sufficient, directly start the specified stage

**Important: mid-entry and Stage 2.5**
- See [P1: Integrity Gate Rules](../shared/pipeline_policies.md#p1-integrity-gate-rules) for skip/passport rules
- See [P4: Review-Only Routing](../shared/pipeline_policies.md#p4-review-only-routing) for review vs check+review distinction

---

## External Review Protocol (Added in v2.5)

**Scenario**: The user submitted to a journal and received feedback from real human reviewers, bringing those comments into the pipeline.

**Trigger**: User says "I received reviewer comments," "reviewer comments," "revise and resubmit," etc.

### Differences from Internal Review

| Aspect | Internal Review (Stage 3 simulation) | External Review (real journal) |
|--------|-------------------------------------|-------------------------------|
| Source of review comments | Pipeline's AI reviewers | Journal's human reviewers |
| Comment format | Structured (Revision Roadmap) | Unstructured (free text, PDF, email) |
| Comment quality | Consistent, predictable | Variable quality, may be vague or contradictory |
| Revision strategy | Can accept wholesale | Need to judge which to accept/reject/negotiate |
| Acceptance criteria | AI re-review suffices | Ultimately decided by human reviewers |

### Step 1: Intake and Structuring

```
1. Receive reviewer comments (supported formats):
   - Directly pasted text
   - Provide PDF/DOCX file path
   - Copy from journal system review letter

2. Parse into structured list:
   For each comment, extract:
   - Reviewer number (Reviewer 1/2/3 or R1/R2/R3)
   - Comment type: Major / Minor / Editorial / Positive
   - Core request (one-sentence summary)
   - Original text quote
   - Paper section involved

3. Produce External Review Summary:
   +----------------------------------------+
   | External Review Summary                |
   +----------------------------------------+
   | Journal: [journal name]                |
   | Decision: [R&R / Major / Minor]        |
   | Reviewers: [N]                         |
   | Total comments: [N]                    |
   |   Major: [n]  Minor: [n]  Editorial: [n]|
   +----------------------------------------+

4. Confirm parsing results with user:
   "I organized the reviewer comments into [N] items. Here is the summary — please confirm nothing was missed or misinterpreted."
```

### Step 2: Strategic Revision Coaching (External Revision Coaching)

Unlike the Socratic coaching for internal review, external review coaching focuses more on **strategic judgment**:

```
For each Major comment, guide the user to think through:

1. Understanding layer
   "What is this reviewer's core concern? Is it about methodology, theory, or presentation?"

2. Judgment layer
   "Do you agree with this criticism?"
   - Agree -> "How do you plan to revise?"
   - Partially agree -> "Which parts do you agree with and which not? What is your basis for disagreement?"
   - Disagree -> "What is your rebuttal argument? Can you support it with literature or data?"

3. Strategy layer
   "How will you phrase this in the response letter?"
   - Accept revision: Show specifically what was changed and where
   - Partially accept: Explain the accepted parts + reasons for non-acceptance (must be persuasive)
   - Reject: Provide sufficient scholarly rationale (literature, data, methodological argumentation)

4. Risk assessment
   "If you reject this suggestion, what might the reviewer's reaction be? Is it worth the risk?"
```

**Key principles**:
- **Do not default to "accept all"**: Real reviewer comments are not always correct — some may be based on misunderstanding or school-of-thought bias
- **Encourage user to inject context**: "What school of thought do you think this reviewer might come from? What context might they not be aware of?"
- **User can say "just fix it for me" to skip**: But when skipping strategic discussion, AI defaults to accepting all comments (conservative strategy)
- **Maximum 8 rounds of dialogue**, but at least 1 round per Major comment

### Step 3: Revision and Response to Reviewers

```
Produce two documents:

1. Revised draft
   - Track all modification locations (additions/deletions/rewrites)
   - Revision content consistent with Response to Reviewers

2. Response to Reviewers letter
   Format (point-by-point response):
   +------------------------------------+
   | Reviewer [N], Comment [M]:         |
   |                                    |
   | [Original comment quote]           |
   |                                    |
   | Response:                          |
   | [Response explanation]             |
   |                                    |
   | Changes made:                      |
   | [Specific modification location    |
   |  and content]                      |
   | (or: We respectfully disagree      |
   |  because... [rationale])           |
   +------------------------------------+
```

### Step 4: Self-Verification (Completeness Check)

```
Stage 3' behavior adjustments in external review mode:

1. Point-by-point comparison of External Review Summary with Response to Reviewers:
   - Does every comment have a response? (completeness)
   - Is each response consistent with actual changes? (consistency)
   - Were the places claimed as "modified" actually changed? (truthfulness)

2. New citation verification:
   - New references added during revision enter Stage 4.5 integrity verification

3. Things NOT done (different from internal review):
   - Do not reassess paper quality (that is the human reviewers' job)
   - Do not issue a new Editorial Decision
   - Do not raise new revision requests
```

### Honest Capability Boundaries

1. **AI verification does not equal human reviewer satisfaction**: Stage 3' can confirm revisions are "complete and consistent," but cannot predict whether human reviewers will accept your responses. Reviewers may have unstated expectations, school-of-thought preferences, or methodological insistence
2. **Unstructured comments may not parse perfectly**: Some reviewers write vaguely (e.g., "the methodology needs more work"), and AI will do its best to parse but may miss implied intentions. After parsing, **user confirmation is mandatory**
3. **AI cannot make scholarly judgments for you**: "Should I accept Reviewer 2's suggestion?" is your decision. AI can provide an analytical framework, but final judgment rests with the researcher
4. **Cross-cultural review convention differences**: Response conventions differ across journals/academic circles (some require extreme deference, others accept direct rebuttal). AI defaults to neutral academic tone; the user can request adjustments

---

## Progress Dashboard

Users can say "status" or "pipeline status" at any time to view:

```
+=============================================+
|   Academic Pipeline v3.0 Status             |
+=============================================+
| Topic: Impact of AI on Higher Education     |
|        Quality Assurance                    |
+---------------------------------------------+

  Stage 1   RESEARCH          [v] Completed
  Stage 2   WRITE             [v] Completed
  Stage 2.5 INTEGRITY         [v] PASS (62/62 refs verified)
  Stage 3   REVIEW (1st)      [v] Major Revision (5 items)
  Stage 3.5 HUMAN REVIEW GATE [v] Continued (AI-only)
  Stage 4   REVISE            [v] Completed (5/5 addressed)
  Stage 3'  RE-REVIEW (2nd)   [v] Accept
  Stage 4'  RE-REVISE         [-] Skipped (Accept)
  Stage 4.5 FINAL INTEGRITY   [..] In Progress
  Stage 5   FINALIZE          [ ] Pending
  Stage 6   PROCESS SUMMARY   [ ] Pending

+---------------------------------------------+
| Integrity Verification:                     |
|   Pre-review:  PASS (0 issues)              |
|   Final:       In progress...               |
+---------------------------------------------+
| Review History:                             |
|   Round 1: Major Revision (5 required)      |
|   Round 2: Accept                           |
+=============================================+
```

See `templates/pipeline_status_template.md` for the output template.

---

## Revision Loop Management

- Stage 3 (first review) -> Stage 4 (revision) -> Stage 3' (verification review) -> Stage 4' (re-revision, if needed) -> Stage 4.5 (final verification)
- **Maximum 1 round of RE-REVISE** (Stage 4'): If Stage 3' gives Major, enter Stage 4' for revision then proceed directly to Stage 4.5 (no return to review)
- **Pipeline overrides paper-writing's max 2 revision rule**: In the pipeline, revisions are limited to Stage 4 + Stage 4' (one round each), replacing paper-writing's max 2 rounds rule
- Mark unresolved issues as Acknowledged Limitations
- Provide cumulative revision history (each round's decision, items addressed, unresolved items)

---

## Reproducibility

v2.0 design ensures consistent quality assurance with each execution:

### Standardized Workflow

| Guarantee Item | Mechanism |
|---------------|-----------|
| Integrity check every time | Per [P1](../shared/pipeline_policies.md#p1-integrity-gate-rules): Stage 4.5 always full; Stage 2.5 reducible only with valid passport + explicit confirmation |
| Consistent review angles | EIC + R1/R2/R3 + Devil's Advocate — five fixed perspectives |
| Consistent verification methods | integrity_verification_agent uses standardized search templates |
| Consistent quality thresholds | Integrity check PASS/FAIL criteria are explicit (zero SERIOUS + zero MEDIUM + zero MAJOR_DISTORTION + zero UNVERIFIABLE) |
| Traceable workflow | Every stage's deliverables are recorded, enabling retrospective audit |

### Audit Trail

When the pipeline ends, state_tracker_agent produces a complete audit trail:

```
Pipeline Audit Trail
====================
Topic: [topic]
Started: [time]
Completed: [time]
Total Stages: [X/11]

Stage 1 RESEARCH: [mode] -> [output count]
Stage 2 WRITE: [mode] -> [word count]
Stage 2.5 INTEGRITY: [PASS/PASS_WITH_NOTES/FAIL] -> [refs verified] / [issues found -> fixed]
Stage 3 REVIEW: [decision] -> [items count]
Stage 3.5 HUMAN REVIEW GATE: [paused/human-feedback-entered/human-review-skipped]
Stage 4 REVISE: [items addressed / total]
Stage 3' RE-REVIEW: [decision]
Stage 4' RE-REVISE: [executed / skipped]
Stage 4.5 FINAL INTEGRITY: [PASS/PASS_WITH_NOTES/FAIL] -> [refs verified]
Stage 5 FINALIZE: Ask format style -> MD + DOCX + LaTeX (apa7/ieee/etc.) -> tectonic -> PDF
Stage 6 PROCESS SUMMARY: MD -> LaTeX -> PDF (English)

Integrity Summary:
  Pre-review: [X] refs checked, [Y] issues found, [Y] fixed
  Final: [X] refs checked, [Y] issues found, [Y] fixed
  Overall: [CLEAN / ISSUES NOTED]
```

---

## Stage 6: Process Summary Protocol (Added in v2.4)

**Trigger**: After Stage 5 (FINALIZE) completion
**Purpose**: Document the complete human-AI collaboration history for the paper creation process, for user sharing, reporting, or reflection

### Workflow

```
1. Review session history and compile the following:
   - User's initial instructions (verbatim quote)
   - Key decision points and user interventions at each stage
   - Direction correction moments and reasons
   - Iteration count and review result summaries
   - Intellectual insights raised by the user (e.g., questions that spawned new chapters)
   - Quality requirement evolution (e.g., formatting, tone adjustments)
   - Pipeline statistics (stage count, review rounds, integrity verification count, etc.)

3. Generate Markdown version (paper_creation_process.md / paper_creation_process_en.md)

4. Convert to LaTeX and compile PDF:
   - pandoc MD -> LaTeX body
   - Package complete LaTeX document (with cover page, table of contents, headers/footers)
   - tectonic compile PDF
```

### Required Content in Process Record

| Section | Content |
|---------|---------|
| Paper Information | Title, final deliverables list |
| Stage-by-Stage Process | Input/output/key decisions for each stage, with verbatim user quotes |
| Iteration Details | Review comment summaries, revision items, re-review results |
| Interaction Pattern Summary | User role, Claude role, intervention count, key turning points — statistics table |
| User Key Decisions | Chronological list of every important decision made by the user |
| Key Lessons | Reusable lessons learned from the process |
| **Collaboration Reflection** | **Final chapter: qualitative reflection on human-AI collaboration process, no numerical scores** (see below) |

### Collaboration Reflection (Final Chapter, Mandatory)

A structured qualitative reflection on the human-AI collaboration process. No numerical scores.

#### Format

**Process Summary**
- Total stages completed, user interventions, pipeline iterations

**Key Decisions & Their Impact**
Table documenting each significant user decision, stage, what changed, and impact on output

**What Worked Well**
- 2-4 specific behaviors with conversation evidence

**Opportunities for Next Time**  
- 1-3 actionable suggestions (framed as opportunities, not criticisms)

**Human vs AI Contribution**
Which aspects of quality came from human judgment (not achievable by AI independently)?

**AI Limitations Encountered**
Where did AI need correction or produce subpar output? Honest self-assessment, mandatory.

#### What Is REMOVED
- No numerical scores (1-100 or otherwise) for user performance
- No "grading" of collaboration quality
- No bar charts of user scores
- No "Needs Improvement" labels

### Output Specifications

- **Filename**: `paper_creation_process.md`
- **PDF**: `paper_creation_process.pdf`
- **LaTeX template**: `article` class, 12pt, A4, Times New Roman
- **Includes table of contents**: `\tableofcontents`
- **Header**: left = document title (italic), right = date
- **Compilation**: tectonic (same toolchain as Stage 5)

---

## Quality Standards

| Dimension | Requirement |
|-----------|------------|
| Stage detection | Correctly identify user's current stage and available materials |
| Mode recommendation | Recommend appropriate mode based on user preferences and material status |
| Material handoff | Stage-to-stage handoff materials are complete and correctly formatted |
| State tracking | Pipeline state updated in real time; Progress Dashboard accurate |
| **Mandatory checkpoint** | **User confirmation required after each stage completion** |
| **Mandatory integrity check** | **See [P1: Integrity Gate Rules](../shared/pipeline_policies.md#p1-integrity-gate-rules)** |
| No overstepping | Orchestrator does not perform substantive research/writing/reviewing, only dispatching |
| No forcing | User can pause or exit pipeline at any time (integrity skip rules per [P1](../shared/pipeline_policies.md#p1-integrity-gate-rules)) |
| Reproducible | Same input follows the same workflow across different sessions |

---

## Error Recovery

| Stage | Error | Handling |
|-------|-------|---------|
| Intake | Cannot determine entry point | Ask user what materials they have and their goal |
| Stage 1 | literature-review not converging | Suggest mode switch (socratic -> full) or narrow scope |
| Stage 2 | Missing research foundation | Suggest returning to Stage 1 to supplement research |
| Stage 2.5 | Still FAIL after 3 correction rounds | Per [P2](../shared/pipeline_policies.md#p2-integrity-failure-handling): user must resolve or remove items — cannot bypass |
| Stage 3 | Review result is Reject | Provide options: major restructuring (Stage 2) or abandon |
| Stage 4 | Revision incomplete on all items | List unaddressed items; ask whether to continue |
| Stage 3' | Verification still has major issues | Enter Stage 4' for final revision |
| Stage 4' | Issues remain after revision | Mark as Acknowledged Limitations; proceed to Stage 4.5 |
| Stage 4.5 | Final verification FAIL | Per [P2](../shared/pipeline_policies.md#p2-integrity-failure-handling): fix and re-verify (max 3 rounds) |
| Any | User leaves midway | Save pipeline state; can resume from breakpoint next time |
| Any | Skill execution failure | Report error; suggest retry or skip |

---

## Agent File References

| Agent | Definition File |
|-------|----------------|
| pipeline_orchestrator_agent | `agents/pipeline_orchestrator_agent.md` |
| state_tracker_agent | `agents/state_tracker_agent.md` |
| integrity_verification_agent | `agents/integrity_verification_agent.md` |

---

## Reference Files

| Reference | Purpose |
|-----------|---------|
| `references/pipeline_state_machine.md` | Complete state machine definition: all legal transitions, preconditions, actions |
| `references/plagiarism_detection_protocol.md` | Phase D originality verification protocol + self-plagiarism + AI text characteristics |
| `references/mode_advisor.md` | Unified cross-skill decision tree: maps user intent to optimal skill + mode |
| `references/claim_verification_protocol.md` | Phase E claim verification protocol: claim extraction, source tracing, cross-referencing, verdict taxonomy |
| `references/team_collaboration_protocol.md` | Multi-person team coordination: role definitions, handoff protocol, version control, conflict resolution |
| `shared/handoff_schemas.md` | Cross-skill data contracts: 9 schemas for all inter-stage handoff artifacts |

---

## Templates

| Template | Purpose |
|----------|---------|
| `templates/pipeline_status_template.md` | Progress Dashboard output template |

---

## Examples

| Example | Demonstrates |
|---------|-------------|
| `examples/full_pipeline_example.md` | Complete pipeline conversation log (Stage 1-5, with integrity + 2-stage review) |
| `examples/mid_entry_example.md` | Mid-entry example starting from Stage 2.5 (existing paper -> integrity check -> review -> revision -> finalization) |

---

## Output Language

Follows user language. Academic terminology retained in English.

---

## Integration with Other Skills

```
full-workflow dispatches the following skills (does not do work itself):

Stage 1: literature-review
  - socratic mode: Guided research exploration
  - full mode: Complete research report
  - quick mode: Quick research summary

Stage 2: paper-writing
  - plan mode: Socratic chapter-by-chapter guidance
  - full mode: Complete paper writing

Stage 2.5: integrity_verification_agent (Mode 1: pre-review)
Stage 4.5: integrity_verification_agent (Mode 2: final-check)

Stage 3: peer-review
  - full mode: Complete 5-person review (EIC + R1/R2/R3 + Devil's Advocate)

Stage 3': peer-review
  - re-review mode: Verification review (focused on revision responses)

Stage 4/4': paper-writing (revision mode)
Stage 5: paper-writing (format-convert mode)
  - Step 1: Ask user which academic formatting style (APA 7.0 / Chicago / IEEE, etc.)
  - Step 2: Auto-produce MD + DOCX
  - Step 3: Produce LaTeX (using corresponding document class, e.g., apa7 class for APA 7.0)
  - Step 4: After user confirms content is correct, tectonic compiles PDF (final version)
  - Fonts: Times New Roman + Courier New (monospace)
  - PDF must be compiled from LaTeX (HTML-to-PDF is prohibited)
```

---

## Related Skills

| Skill | Relationship |
|-------|-------------|
| `literature-review` | Dispatched (Stage 1 research phase) |
| `paper-writing` | Dispatched (Stage 2 writing, Stage 4/4' revision, Stage 5 formatting) |
| `peer-review` | Dispatched (Stage 3 first review, Stage 3' verification review) |

---

## Version Info

| Item | Content |
|------|---------|
| Skill Version | 3.0 |
| Last Updated | 2026-04-02 |
| Maintainer | Cheng-I Wu |
| Dependent Skills | literature-review v2.0+, paper-writing v2.0+, peer-review v1.1+ |
| Role | Full academic research workflow orchestrator |

---

## Changelog

| Version | Date | Changes |
|---------|------|---------|
| 3.0 | 2026-04-02 | **A+ Redesign**: (1) Added Capability Boundaries section at top — honest disclosure of what the pipeline can and cannot do. (2) New Stage 3.5 Human Review Gate — mandatory pause point after AI self-review to solicit human reviewer feedback, with pause/enter/continue options and state persistence. (3) Replaced Collaboration Quality Evaluation (numerical 1-100 scoring, bar charts, grading) with Collaboration Reflection — qualitative process reflection with no scores or grades. (4) Simplified Checkpoint System — reduced from 3 types (FULL/SLIM/MANDATORY) to 2 (GATE/NOTIFY), removing awareness guard and auto-continue counting. (5) Added File-Based State Persistence via `.pipeline/state.json` for conversation-resilient state tracking. (6) Honest language updates throughout — replaced "100% reference verification" with "systematic reference spot-checking", added "(within automated verification capabilities)" qualifiers, updated "review" to "structured self-review", "5 review reports" to "5-perspective analysis reports". |
| 2.7 | 2026-03-27 | **Style Profile in Material Passport**: Pipeline orchestrator now carries optional Style Profile (Schema 10 in `shared/handoff_schemas.md`) through all stages. Produced by paper-writing intake Step 10 when user provides past writing samples. Consumed by draft_writer (Stage 2) and report_compiler (Stage 1) as soft writing voice guide. Does not affect integrity verification or review stages. Coordinates with literature-review v2.4 and paper-writing v2.5 |
| 2.6 | 2026-03-08 | **Handoff Data Schema**: Enhanced `shared/handoff_schemas.md` with 9 comprehensive schemas (RQ Brief, Bibliography, Synthesis, Paper Draft, Integrity Report, Review Report, Revision Roadmap, Response to Reviewers, Material Passport) with full field definitions, type constraints, and validation rules; orchestrator validates output against schemas before each transition. **Adaptive Checkpoint System**: Replaced static checkpoint template with 3-tier system (FULL/SLIM/MANDATORY) based on stage criticality and user engagement; FULL checkpoints include decision dashboard with metrics; SLIM auto-continues for experienced users; MANDATORY cannot be bypassed at integrity/review/finalization boundaries; awareness guard after 4+ auto-continues. **Mode Advisor**: New `references/mode_advisor.md` with unified cross-skill decision tree, common misconceptions table, user archetype recommendations, decision flowchart, and anti-patterns guide. **Team Collaboration Protocol**: New `references/team_collaboration_protocol.md` with 5 role definitions, per-transition handoff procedures, git branching/tagging strategy, conflict resolution matrix, and communication templates; state tracker extended with `assigned_to`, `approval_gate`, `team_notes` per stage and `schema_validation_log`. **Phase E Claim Verification**: New `references/claim_verification_protocol.md` with E1 claim extraction, E2 source tracing, E3 cross-referencing; verdict taxonomy (VERIFIED / MINOR_DISTORTION / MAJOR_DISTORTION / UNVERIFIABLE / UNVERIFIABLE_ACCESS); severity mapping (MAJOR_DISTORTION -> SERIOUS, UNVERIFIABLE -> SERIOUS, MINOR_DISTORTION -> MINOR, UNVERIFIABLE_ACCESS -> MEDIUM); integrated into integrity_verification_agent Mode 1 (30% spot-check) and Mode 2 (100%); pass/fail criteria updated to include Phase E verdicts. **Mid-Entry Material Passport Check**: Pipeline orchestrator now validates Material Passport on mid-entry; decision tree checks verification_status, freshness (< 24 hours), and content modification (version_label comparison); offers skip/spot-check/full re-verify options for Stage 2.5 when passport is valid; passport freshness validation rules added to `shared/handoff_schemas.md` |
| 2.5 | 2026-03-08 | External Review Protocol: structured intake of real journal reviewer feedback (text/PDF/DOCX); 4-step workflow (parse -> strategic coaching -> revise + Response to Reviewers -> completeness check); differentiated behavior from internal simulated review (no default "accept all", risk assessment per comment, user confirmation of parsed items); explicit capability boundaries (AI verification ≠ reviewer satisfaction) |
| 2.4 | 2026-03-08 | Stage 6 PROCESS SUMMARY: post-pipeline paper creation process record; asks user preferred language (zh/en/both); generates structured MD summarizing full human-AI collaboration history with user quotes, key decisions, iteration details, and lessons learned; mandatory final chapter: **Collaboration Quality Evaluation** (6 dimensions scored 1-100, bar chart visualization, What Worked Well / Missed Opportunities / Recommendations / Human vs AI Value-Add / Claude's Self-Reflection); compiles to PDF via LaTeX + tectonic; outputs `paper_creation_process_zh.pdf` + `paper_creation_process_en.pdf` |
| 2.3 | 2026-03-08 | Stage 5 FINALIZE: mandatory formatting style prompt (APA 7.0 / Chicago / IEEE); PDF must compile from LaTeX via tectonic (no HTML-to-PDF); APA 7.0 uses `apa7` document class (`man` mode); font stack: Times New Roman + Courier New |
| 2.2 | 2025-03-05 | Checkpoint confirmation semantics (6 user commands with precise actions); mode switching rules (safe/dangerous/prohibited matrix); skill failure fallback matrix (per-stage degradation strategies); state ownership protocol (single source of truth with write access control); material version control (versioned artifacts with audit trail); cross-skill reference to `shared/handoff_schemas.md` |
| 2.1 | 2026-03 | Added plagiarism detection protocol (Phase D); enhanced integrity_verification_agent with originality verification (D1 WebSearch, D2 self-plagiarism); updated both verification modes |
| 2.0 | 2026-02 | Added Stage 2.5/4.5 integrity checks, two-stage review, mandatory checkpoints, Devil's Advocate, reproducibility guarantees, integrity_verification_agent |
| 1.0 | 2026-02 | Initial version: 5+1 stage pipeline |
