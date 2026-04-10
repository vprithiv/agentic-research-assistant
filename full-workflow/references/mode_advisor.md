# Mode Advisor — Unified Cross-Skill Decision Tree

## Purpose

Helps users (and the pipeline orchestrator) select the right skill and mode for their current situation. Eliminates the most common routing mistakes by mapping user intent to the optimal entry point.

---

## Quick Decision Matrix

| What do you want? | How far along? | Time? | Skill + Mode |
|-------------------|---------------|-------|--------------|
| Explore a topic | Starting fresh | 30 min | literature-review quick |
| Explore a topic | Starting fresh | 2+ hr | literature-review full |
| Think through a research idea | Have vague idea | Any | literature-review socratic |
| Systematic review | Have clear PICO | 3+ hr | literature-review systematic-review |
| Verify claims | Have specific claims | 30 min | literature-review fact-check |
| Write a paper | Have research done | 2+ hr | paper-writing full |
| Plan a paper step by step | Have RQ, need structure | 1+ hr | paper-writing plan |
| Fix citations | Have draft | 30 min | paper-writing citation-check |
| Convert format | Have final draft | 15 min | paper-writing format-convert |
| Review a paper | Have paper to evaluate | 1 hr | peer-review full |
| Check revision quality | Have revised draft | 30 min | peer-review re-review |
| Full pipeline (zero to publication) | Starting fresh | 5+ hr | full-workflow |
| Handle real reviewer feedback | Have review comments | 1+ hr | full-workflow (Stage 4 entry) |

---

## Common Misconceptions

| User Says | They Probably Need | Why |
|-----------|-------------------|-----|
| "Write me a paper on X" | literature-review first, THEN paper-writing | Writing without research produces shallow papers with unsupported claims |
| "Review my paper" (but no draft exists) | paper-writing plan mode | They need to write first, not review |
| "Check my citations" (but paper isn't done) | paper-writing full mode | Finish writing first, then check citations as a separate pass |
| "I need a systematic review" | literature-review systematic-review mode | NOT paper-writing lit-review structure (different methodology: PRISMA vs narrative) |
| "Just give me a quick paper" | literature-review quick + paper-writing full | Quick research is fine, but paper writing still needs the full mode for quality |
| "Format my paper as APA" | paper-writing format-convert mode | Not a rewrite; purely formatting transformation |
| "I got reviewer comments" | full-workflow Stage 4 entry (External Review) | Needs structured intake + strategic coaching, not just "fix what they said" |

---

## User Archetype Recommendations

| Archetype | Recommended Workflow | Rationale |
|-----------|---------------------|-----------|
| Graduate student (first paper) | literature-review socratic -> paper-writing plan -> full pipeline | Socratic mode builds research thinking; plan mode structures the paper incrementally; pipeline ensures quality gates |
| Experienced researcher (submission prep) | full-workflow (full, from Stage 1 or mid-entry) | Knows what they want; benefits from the automated quality assurance and integrity checks |
| Advisor reviewing student work | peer-review full | Provides structured multi-perspective feedback the advisor can use in mentoring |
| Quick literature scan | literature-review quick or lit-review | Fast turnaround; no need for full pipeline overhead |
| Journal revision response | full-workflow (Stage 4 entry with review comments) | External Review Protocol handles real reviewer feedback with strategic coaching |
| Conference paper (short deadline) | literature-review quick -> paper-writing full (conference type) | Compressed timeline; quick research + full writing with conference structure |
| Thesis chapter | literature-review full -> paper-writing full | Each chapter treated as a standalone paper; full depth needed |
| Policy brief | literature-review quick -> paper-writing full (policy_brief type) | Evidence-based but concise; quick research sufficient for policy scope |

---

## Skill Capability Boundaries

Understanding what each skill can and cannot do prevents misrouting:

| Skill | Can Do | Cannot Do |
|-------|--------|-----------|
| literature-review | Literature search, synthesis, RQ refinement, fact-checking | Write papers, review papers, format documents |
| paper-writing | Write papers, revise papers, format documents, check citations | Conduct original research, review papers (as reviewer), verify integrity |
| peer-review | Review papers (5-person panel), re-review revisions | Write papers, conduct research, fix issues (only identifies them) |
| full-workflow | Orchestrate all stages, manage transitions, track state | Perform any substantive work (purely dispatching and coordinating) |
| integrity_verification_agent | Verify references, citations, data, originality | Fix issues (only identifies them), review paper quality |

---

## Decision Flowchart

```
START: What does the user want?
  |
  +--> "I want to research/explore/investigate"
  |      |
  |      +--> Have specific claims to verify? --> literature-review fact-check
  |      +--> Have clear PICO/systematic question? --> literature-review systematic-review
  |      +--> Want guided exploration? --> literature-review socratic
  |      +--> Want direct results, have time? --> literature-review full
  |      +--> Want direct results, short on time? --> literature-review quick
  |
  +--> "I want to write a paper"
  |      |
  |      +--> Have research/literature ready? --> paper-writing (plan or full)
  |      +--> No research done yet? --> literature-review FIRST, then paper-writing
  |      +--> Want full quality assurance? --> full-workflow (from Stage 1)
  |
  +--> "I want someone to review my paper"
  |      |
  |      +--> Have a complete draft? --> peer-review full
  |      +--> Want integrity check + review? --> full-workflow (Stage 2.5 entry)
  |      +--> No draft yet? --> paper-writing first
  |
  +--> "I need to revise based on feedback"
  |      |
  |      +--> From AI reviewers (pipeline)? --> Continue pipeline (Stage 4)
  |      +--> From real journal reviewers? --> full-workflow Stage 4 entry (External Review)
  |
  +--> "I want the full treatment (research to publication)"
         |
         +--> full-workflow (Stage 1 entry)
```

---

## Pipeline Stage Entry Points

For users entering the pipeline mid-stream, this table clarifies what materials are needed:

| Entry Point | Required Materials | What Gets Skipped | Integrity Implications |
|------------|-------------------|-------------------|----------------------|
| Stage 1 (RESEARCH) | None | Nothing | Full pipeline |
| Stage 2 (WRITE) | RQ Brief + Bibliography | Stage 1 | Full pipeline from Stage 2 |
| Stage 2.5 (INTEGRITY) | Paper draft | Stages 1-2 | Integrity check runs on provided draft |
| Stage 3 (REVIEW) | Verified paper + integrity report | Stages 1-2.5 | User must provide integrity evidence |
| Stage 4 (REVISE) | Paper + review comments | Stages 1-3 | Pipeline runs Stage 4 -> 3' -> 4' -> 4.5 -> 5 |
| Stage 5 (FINALIZE) | Paper + integrity pass report | Stages 1-4.5 | Must show Stage 4.5 passed |

---

## Anti-Patterns

These are common workflow mistakes to avoid:

| Anti-Pattern | Problem | Correct Approach |
|-------------|---------|-----------------|
| Skipping research | Paper lacks evidence depth | Always do at least literature-review quick |
| Writing then researching | Confirmation bias in source selection | Research first, write second |
| Reviewing before integrity check | Wasted review effort on fabricated citations | Always Stage 2.5 before Stage 3 |
| Accepting all reviewer comments blindly | May introduce inconsistencies or weaken valid arguments | Use External Review Protocol's strategic coaching |
| Running pipeline for a 1-page abstract | Overhead far exceeds benefit | Use paper-writing full directly |
| Using fact-check mode for literature review | Different purpose and methodology | Use literature-review full or systematic-review |
