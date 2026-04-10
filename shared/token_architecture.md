# Token Management Architecture

> Canonical reference for context budget allocation, agent loading, and execution patterns across all academic research skills.

---

## Context Budget Allocation

Full pipeline: **200K usable tokens** distributed across 11 stages.

| # | Stage | Budget | Cumulative |
|---|-------|--------|------------|
| 1 | Orchestrator bootstrap | 3K | 3K |
| 2 | Research | 15K | 18K |
| 3 | Literature | 25K | 43K |
| 4 | Synthesis | 20K | 63K |
| 5 | Drafting | 30K | 93K |
| 6 | References | 10K | 103K |
| 7 | Review (x5 perspectives) | 50K (10K each) | 153K |
| 8 | Review synthesis | 12K | 165K |
| 9 | Revision | 20K | 185K |
| 10 | Final check & export | 15K | 200K |

**Rules:**
- Each stage MUST stay within its budget. If a stage finishes under budget, surplus is NOT carried forward — it serves as buffer for unexpected re-reads.
- Monitor token usage at phase boundaries. If a stage consumes >80% of budget before completion, trigger Context Compaction Protocol (see below).
- Stages 7a-7e (individual reviews) are isolated — each reviewer gets a clean 10K allocation.

---

## Three-Tier Agent Representation

### Tier 1: Router Table (~500 tokens total)

Single registry file (`shared/agent_registry.md`) containing:
- Agent name
- File path
- One-line role description

**Load at:** Pipeline start. Keep in context for entire run.

### Tier 2: Compressed Agent Cards (~150-300 tokens each)

Telegraphic instructions. No prose. Behavioral directives only.

Format:
```
ROLE: [one line]
INPUTS: [list]
OUTPUTS: [list]
CONSTRAINTS: [bullet list, imperative mood]
TOOLS: [allowed tool list]
STOP WHEN: [exit condition]
```

**Load at:** Phase start. Unload at phase end.

### Tier 3: Full Definition (original .md file)

Complete agent definition with rationale, examples, edge cases.

**Load ONLY IF:** Tier 2 card is insufficient for the task at hand (ambiguous input, unusual domain, error recovery).

**Escalation trigger:** Agent produces malformed output or requests clarification on a directive.

---

## Lazy Loading Protocol

### Rule: Never load more than 3 agent definitions simultaneously.

### Per-Phase Loading Schedule

**literature-review:**
| Phase | Agents Loaded | Agents Released |
|-------|---------------|-----------------|
| Scoping | research_question_agent, research_architect_agent | — |
| Search | bibliography_agent, source_verification_agent | research_question_agent, research_architect_agent |
| Synthesis | synthesis_agent | bibliography_agent, source_verification_agent |
| Drafting | report_compiler_agent | synthesis_agent |
| Review | editor_in_chief_agent, devils_advocate_agent | report_compiler_agent |
| Ethics/Bias | ethics_review_agent, risk_of_bias_agent | editor_in_chief_agent, devils_advocate_agent |
| Meta-analysis (if triggered) | meta_analysis_agent | ethics_review_agent, risk_of_bias_agent |
| Dialogue (if interactive) | socratic_mentor_agent | all others |
| Monitoring | monitoring_agent | (co-loaded as needed) |

**paper-writing:**
| Phase | Agents Loaded | Agents Released |
|-------|---------------|-----------------|
| Intake | intake_agent | — |
| Literature | literature_strategist_agent | intake_agent |
| Structure | structure_architect_agent, argument_builder_agent | literature_strategist_agent |
| Drafting | draft_writer_agent | structure_architect_agent, argument_builder_agent |
| Compliance | citation_compliance_agent | draft_writer_agent |
| Abstract | abstract_agent | citation_compliance_agent |
| Self-check | peer_reviewer_agent | abstract_agent |
| Visualization | visualization_agent | peer_reviewer_agent |
| Formatting | formatter_agent | visualization_agent |
| Revision (if triggered) | revision_coach_agent | formatter_agent |
| Dialogue (if interactive) | socratic_mentor_agent | all others |

**peer-review:**
| Phase | Agents Loaded | Agents Released |
|-------|---------------|-----------------|
| Triage | eic_agent | — |
| Review round | ONE reviewer agent at a time | previous reviewer |
| Field analysis | field_analyst_agent | last reviewer |
| Synthesis | editorial_synthesizer_agent | field_analyst_agent |

**full-workflow:**
| Phase | Agents Loaded | Agents Released |
|-------|---------------|-----------------|
| Orchestration | pipeline_orchestrator_agent | — |
| Verification | integrity_verification_agent | (co-loaded with orchestrator) |
| Delegation | pipeline_orchestrator_agent + 1 skill agent | integrity_verification_agent |

### Stage Manifest Pattern

At each phase boundary, write a manifest file:

```
File: {project_dir}/state/stage_{N}_manifest.json
{
  "stage": N,
  "agents_loaded": ["agent_a", "agent_b"],
  "inputs_read": ["file_path_1", "file_path_2"],
  "outputs_written": ["file_path_3"],
  "tokens_used_estimate": "12K",
  "next_stage": N+1,
  "next_agents": ["agent_c"]
}
```

---

## Read-Process-Write-Forget Pattern

This is the fundamental memory management pattern for all stages.

### Steps:

1. **LOAD** — Read specific input files from disk into context.
2. **PROCESS** — Perform cognitive work (analysis, synthesis, generation) in-context.
3. **WRITE** — Write structured output to disk immediately. Do not defer.
4. **FORGET** — In subsequent reasoning, reference the output file path only. Do NOT re-quote content.

### Example:

```
# LOAD
Read: state/literature_results.json

# PROCESS
[Synthesis work happens here in-context]

# WRITE
Write to: state/synthesis_output.md

# FORGET
Subsequent references use: "See state/synthesis_output.md, sections 2-4"
NOT: "As noted in the synthesis, the three themes were..."
```

### Critical Rules:
- NEVER hold two large documents in context simultaneously if one has already been processed.
- ALWAYS write intermediate results before loading new inputs.
- File paths ARE the memory. The context window is the workspace, not the archive.

---

## Sequential Isolation Protocol (Reviews)

Purpose: Prevent anchoring bias between reviewers.

### Standard Isolation

Each reviewer receives ONLY:
1. The paper under review (or relevant sections)
2. Their own agent card (Tier 2)
3. The anti-anchoring instruction block (below)

Each reviewer NEVER receives:
- Other reviewers' outputs
- Previous review scores
- Synthesis drafts

### Anti-Anchoring Instruction Block

Include at the start of each reviewer's context:

```
ISOLATION NOTICE: You are one of several analytical perspectives in a structured self-review.
- You have NOT seen other perspectives' outputs. Do not speculate about them.
- Base your assessment SOLELY on the paper and your assigned expertise domain.
- Score independently. Do not hedge toward imagined consensus.
- Write your review DIRECTLY to file before any other output.
```

### Review Output Protocol

Each reviewer writes directly to:
```
{project_dir}/reviews/review_{perspective_name}.md
```

No intermediate summarization. No cross-reviewer comparison until synthesis phase.

### Default: Subprocess Isolation (Required in Pipeline Mode)

When running within the full-workflow (Stage 3), each reviewer MUST run as an isolated subprocess to guarantee true context separation:

```bash
claude --model opus --print -p "You are {agent_role}. Review this paper: {paper_content}. {anti_anchoring_block}. Write review to {output_path}."
```

This provides true context isolation — each reviewer literally cannot see other reviews. Note: `--print` is safe here because reviewers do NOT need tool access (no WebSearch/WebFetch). They receive the paper text in the prompt and write their review to stdout.

**When standalone** (peer-review without pipeline): Sequential in-context execution is acceptable if subprocess launching is impractical, but the anti-anchoring instruction block is mandatory and reviewers must write to file before any other output.

---

## Batched Verification Protocol

For reference/citation verification in the integrity stage.

### Triage Rules (apply in order):

| Condition | Action |
|-----------|--------|
| DOI present | WebFetch the DOI URL directly |
| Specific title + author | Single WebSearch query |
| Vague reference (no title, no DOI) | Flag as `MANUAL_CHECK_REQUIRED` |
| Book (ISBN or publisher known) | Skip verification, flag as `BOOK_NOT_VERIFIED` |

### Batch Processing:
- Process references in batches of **10**.
- After each batch, write results before starting next batch.
- Do NOT accumulate all verification results in context.

### Output Format:

Each reference produces a single-line entry in `verification_log.jsonl`:

```json
{"ref_id": "R12", "verified": true, "actual_title": "...", "actual_year": 2023, "doi": "10.1234/...", "discrepancy_notes": null}
{"ref_id": "R13", "verified": false, "actual_title": null, "actual_year": null, "doi": null, "discrepancy_notes": "Title not found via WebSearch; possible hallucination"}
```

### Budget: 10K tokens for up to ~50 references. If >50 references, prioritize:
1. References supporting key claims
2. References in the abstract/introduction
3. Remaining references by order of appearance

---

## Chunked Execution Patterns

### Pattern A: Long Document Generation

**Problem:** Generating a full paper in one pass exceeds context budget and degrades quality.

**Solution:** Section-by-section generation.

```
For each section in outline:
  1. Load: outline + previous section's last paragraph (for continuity)
  2. Generate: current section only
  3. Write: section to disk
  4. Release: section content from context
  5. Carry forward: section file path + 2-sentence summary only
```

### Pattern B: Large-Scale Literature Search

**Problem:** Running many search queries accumulates results beyond budget.

**Solution:** Batches of 3 queries with intermediate filtering.

```
For each batch of 3 queries:
  1. Execute 3 WebSearch calls
  2. Screen results against inclusion criteria
  3. Write passing results to state/literature_batch_{N}.json
  4. Release raw search results from context
  5. Carry forward: count of results + file path only
```

### Pattern C: Two-Tier Literature Screening (Compressed Returns)

**Problem:** Screening 50+ candidate sources with full annotations (5 fields, ~150 tokens each) consumes 7,500+ tokens during Pass 1, when most will be excluded.

**Solution:** Compressed screening in Pass 1, full annotation only for survivors in Pass 2.

```
Pass 1 — Compressed Screening (~30 tokens/source):
  For each batch of search results:
    1. Extract compressed entry: ID + title_short + TL;DR + year + DOI + tags
    2. Screen against inclusion/exclusion criteria using ONLY compressed fields
    3. Tag: Include / Exclude / Maybe
    4. Write compressed entries to working set: state/working_set.json
    5. Release raw search results from context
    6. Carry forward: working set handle + entry count only

Pass 2 — Full Annotation (included + maybe sources only):
  For each source with status "included" or "pending_fulltext":
    1. Load: source abstract/full-text (one at a time)
    2. Generate: full annotation (relevance, key findings, methodology, quality, contribution)
    3. Write: expanded entry to state/working_set_expanded/{id}.json
    4. Release: source text from context
    5. Update: working set entry status → "included" (final) or "excluded"
```

**Token savings:** For 50 candidates filtered to 20:
- Current: 50 × 150 = 7,500 tokens (all annotated)
- Two-tier: (50 × 35) + (20 × 150) = 1,750 + 3,000 = 4,750 tokens
- Savings: **~37% per search round**, compounding across 3-4 rounds

### Pattern D: Working Set Grep (Cross-Cutting Analysis)

**Problem:** Identifying patterns across 20-30 collected sources requires re-reading full texts or relying on annotations from memory.

**Solution:** Use the Grep tool directly on working set files for rapid cross-reference before loading full texts.

```
Pre-synthesis pattern discovery:
  1. Grep state/working_set.json for each key concept in the RQ
     (searches across all TL;DRs and tags simultaneously)
  2. Grep state/working_set_expanded/*.json for methodology terms:
     e.g., "FEM|FEA|phase-field|XFEM|cohesive zone"
  3. Grep for V&V terms: "convergence|mesh independence|validation|benchmark"
  4. Tabulate: which source IDs mention which terms
  5. Write cross-reference table to state/cross_reference_matrix.md
  6. Load full annotations ONLY for sources appearing in unexpected combinations
```

**Token savings:** 10-20% reduction in synthesis phase. Grep is a tool call (zero model tokens). Only sources with interesting patterns get full-loaded.

### Pattern E: Batched Verification (Tool-Assisted)

**Problem:** Verifying N references sequentially accumulates context and wastes token budget.

**Solution:** Batched in-context verification using the parent process's WebFetch and WebSearch tools. Each batch is processed and released before the next loads.

> **Important:** `claude --print` subprocesses do NOT have tool access (no WebFetch, no WebSearch). All verification that requires web access must run in the parent conversation context using batched tool calls.

```
Batched verification template:
  1. Partition references into batches of 10
  2. For each batch:
     a. Issue up to 10 parallel WebFetch/WebSearch tool calls
     b. Process results: compare metadata, flag mismatches
     c. Write batch results to state/verification_batch_{N}.jsonl
     d. Release batch from context (Read-Process-Write-Forget)
  3. Merge all batches into state/verification_log.jsonl
```

**Use cases:**

| Operation | Tool | Tokens/batch (10 items) | Batches for 50 refs |
|-----------|------|------------------------|---------------------|
| DOI verification | WebFetch | ~2K | 5 |
| WebSearch source check | WebSearch | ~3K | 5 (50% sample = 25 refs) |
| Combined (Tier 1 + Tier 2) | Both | ~5K | 5 |

**Token savings:** For 50 references:
- Sequential (unbatched): each ref adds ~1,500 tokens of accumulated context = up to 75K
- Batched (10 per batch, release between): 5 batches × ~2-3K = 10-15K
- Savings: **~70-80% in verification phase** (primarily from context release between batches)

**Error handling:** If a tool call fails, log the failure and continue the batch. Retry failed items once at the end. If still failing, flag as `MANUAL_CHECK_REQUIRED`.

### Subprocess Parallel Map (Non-Tool Tasks Only)

For tasks that do NOT require web/tool access (e.g., structured text extraction, metadata comparison, format validation), subprocess parallelism is viable:

```
claude --model {tier} --print -p "{query_template}"
```

**Valid use cases for `--print` subprocesses:**
- Comparing two text strings for similarity (metadata match)
- Extracting structured fields from a block of text
- Format validation (checking citation format compliance)
- Generating reviewer identity configurations

**NOT valid for `--print` subprocesses:**
- DOI resolution (requires WebFetch)
- Source existence verification (requires WebSearch)
- Any task that needs file read/write access

### Pattern F: Revision Pass

**Problem:** Loading full paper + full review for each edit wastes budget.

**Solution:** Targeted loading per edit.

```
For each revision item:
  1. Load: ONLY the target section from paper
  2. Load: ONLY the specific review finding (single paragraph)
  3. Apply edit
  4. Write: revised section to disk
  5. Release both from context
```

---

## Model Cost Optimization

### Per-Stage Model Assignment

| # | Stage | Primary Agent(s) | Model | Token Budget |
|---|-------|-------------------|-------|-------------|
| 1 | Orchestrator bootstrap | pipeline_orchestrator_agent, state_tracker_agent | sonnet, haiku | 3K |
| 2 | Research | research_question_agent, research_architect_agent | sonnet, sonnet | 15K |
| 3 | Literature | bibliography_agent, source_verification_agent | sonnet, sonnet | 25K |
| 4 | Synthesis | synthesis_agent, meta_analysis_agent | opus, opus | 20K |
| 5 | Drafting | argument_builder_agent, draft_writer_agent | opus, opus | 30K |
| 6 | References | citation_compliance_agent, integrity_verification_agent | sonnet, sonnet | 10K |
| 7 | Review (x5 perspectives) | eic, methodology, domain, perspective, devils_advocate | opus (all) | 50K |
| 8 | Review synthesis | editorial_synthesizer_agent | opus | 12K |
| 9 | Revision | revision_coach_agent, formatter_agent | sonnet, sonnet | 20K |
| 10 | Final check & export | editor_in_chief_agent, monitoring_agent | opus, haiku | 15K |

**Cost breakdown:** Stages 4, 5, 7, 8, 10 use Opus (~112K tokens). Stages 1-3, 6, 9 use Sonnet/Haiku (~88K tokens). The biggest cost savings come from stages 1-3, 6, and 9 where structured work dominates.

### Prompt Caching Strategy

Place **static reference content FIRST** in agent prompts, before any dynamic content (paper text, search results, user input). Cached input is billed at ~10% of the standard rate.

**High-value static files to cache** (place at TOP of prompt, in this order):

| File | Size | Used By |
|------|------|---------|
| `shared/handoff_schemas.md` | ~26KB | ALL agents |
| `references/statistical_visualization_standards.md` | ~24KB | visualization, report_compiler, draft_writer |
| `references/methodology_patterns.md` | ~24KB | research_architect, methodology_reviewer, structure_architect |
| `references/statistical_reporting_standards.md` | ~23KB | synthesis, draft_writer, peer_reviewer |
| `references/systematic_review_toolkit.md` | ~19KB | bibliography, source_verification, risk_of_bias |

**Caching rules:**
1. Static reference content FIRST in prompt → eligible for cache hit on subsequent calls.
2. Dynamic content (paper text, search results, user-specific context) AFTER static content.
3. Agent card (Tier 2) placed between static refs and dynamic content.
4. At ~30% cache hit rate across a full pipeline run (conservative: lazy loading and subprocess isolation reduce effective hits), caching saves ~5-8% on input token costs. Note: prompt caching only works within the same API conversation context — subprocesses do not share cache state.

**Estimated combined savings:**

| Optimization | Savings | Phase | Notes |
|-------------|---------|-------|-------|
| Model routing (18 agents → Sonnet, 2 → Haiku) | ~35% | Model routing | Applies to model cost dimension |
| Prompt caching (~116KB static refs, ~30% hit rate) | ~5-8% | Model routing | Conservative: lazy loading works against cache TTL |
| Two-tier screening (Pattern C, compressed returns) | ~3-5% | Working set | ~37% per search round, applied to 25K lit budget |
| Working set grep (Pattern D, pre-synthesis filtering) | ~3-5% | Working set | Zero model tokens; reduces full-annotation reads |
| Batched verification (Pattern E, context release) | ~3-4% | Verification | Batch-and-release vs. accumulated context |
| Research session continuity (Schema 12, no duplicate searches) | ~3-5% | Session state | Depends on literature-review → paper-writing overlap |
| **Combined** | **~45-52%** | All | Individual savings target different cost dimensions; not simply additive |

---

## Context Compaction Protocol

**Trigger:** Context usage exceeds 80% of stage budget, OR transitioning between major phases.

### Steps:

1. **Write all current state to disk.** Every intermediate result, plan, list, or draft goes to a file.
2. **Produce a stage summary** (~500 tokens max):
   ```
   ## Stage {N} Summary
   - Completed: [what was done]
   - Key outputs: [file paths]
   - Decisions made: [list]
   - Open items: [list]
   - Next stage inputs needed: [file paths]
   ```
3. **Write summary to:** `state/stage_{N}_summary.md`
4. **Subsequent processing references summary file path.** Do not re-read full state unless required for a specific operation.

### Compaction Quality Check:
Before discarding context, verify:
- [ ] All outputs written to disk
- [ ] Summary captures all decisions (not just results)
- [ ] File paths in summary are correct and files exist
- [ ] No orphaned state (information only in context, not on disk)
