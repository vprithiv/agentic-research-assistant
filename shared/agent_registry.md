# Agent Registry (Tier 1 Router)

> Load this file ONCE at pipeline start. Load individual agent cards ONLY when their phase begins.
> Total agents: 35. This file: ~500 tokens. Do NOT load full agent definitions from here.

---

## literature-review (13 agents)

| Agent | File | Role | Model |
|-------|------|------|-------|
| research_question_agent | literature-review/agents/research_question_agent.md | RQ formulation + scoping | sonnet |
| research_architect_agent | literature-review/agents/research_architect_agent.md | Methodology blueprint + research design | sonnet |
| bibliography_agent | literature-review/agents/bibliography_agent.md | Search, screen, grade sources | sonnet |
| source_verification_agent | literature-review/agents/source_verification_agent.md | Verify source authenticity + accuracy | sonnet |
| synthesis_agent | literature-review/agents/synthesis_agent.md | Cross-source synthesis + gap analysis | opus |
| report_compiler_agent | literature-review/agents/report_compiler_agent.md | APA 7.0 report drafting | sonnet |
| editor_in_chief_agent | literature-review/agents/editor_in_chief_agent.md | Editorial review + quality control | opus |
| devils_advocate_agent | literature-review/agents/devils_advocate_agent.md | Challenge assumptions, logic check | opus |
| socratic_mentor_agent | literature-review/agents/socratic_mentor_agent.md | Guided research dialogue | opus |
| ethics_review_agent | literature-review/agents/ethics_review_agent.md | Ethics review + compliance | sonnet |
| risk_of_bias_agent | literature-review/agents/risk_of_bias_agent.md | Risk of bias assessment | sonnet |
| meta_analysis_agent | literature-review/agents/meta_analysis_agent.md | Meta-analysis support | opus |
| monitoring_agent | literature-review/agents/monitoring_agent.md | Pipeline monitoring + progress tracking | haiku |

> **Computational Mechanics / Materials Science Override:** When the user's field is computational mechanics or computational materials science, all literature-review agents should: (1) Use Pattern 7 from `paper_structure_patterns.md` (Computational/Modeling) as the default report structure — note: this is distinct from Pattern 7 in `methodology_patterns.md` (Benchmarking Study); (2) Default to numbered citations (not APA author-date); (3) Ask for research *objectives*, not research *questions*; (4) Prioritize verification and validation (V&V) assessment in methodology evaluation -- treat missing V&V as a CRITICAL gap;

## paper-writing (12 agents)

| Agent | File | Role | Model |
|-------|------|------|-------|
| intake_agent | paper-writing/agents/intake_agent.md | Config interview + plan mode guidance | sonnet |
| literature_strategist_agent | paper-writing/agents/literature_strategist_agent.md | Paper-context literature search | sonnet |
| structure_architect_agent | paper-writing/agents/structure_architect_agent.md | Outline + argument construction | sonnet |
| argument_builder_agent | paper-writing/agents/argument_builder_agent.md | Argument development + evidence mapping | opus |
| draft_writer_agent | paper-writing/agents/draft_writer_agent.md | Section drafting | opus |
| citation_compliance_agent | paper-writing/agents/citation_compliance_agent.md | Citation audit + compliance | sonnet |
| abstract_agent | paper-writing/agents/abstract_agent.md | Abstract generation | sonnet |
| peer_reviewer_agent | paper-writing/agents/peer_reviewer_agent.md | Internal peer review | opus |
| formatter_agent | paper-writing/agents/formatter_agent.md | Output format conversion | sonnet |
| socratic_mentor_agent | paper-writing/agents/socratic_mentor_agent.md | Guided writing dialogue | opus |
| visualization_agent | paper-writing/agents/visualization_agent.md | Figure + table generation | sonnet |
| revision_coach_agent | paper-writing/agents/revision_coach_agent.md | Revision guidance + coaching | sonnet |

> **Computational Mechanics / Materials Science Override:** When the user's field is computational mechanics or computational materials science, all paper-writing agents should: (1) Use Pattern 7 (Computational/Modeling) as the default paper structure; (2) Default to numbered citations (not APA author-date); (3) Ask for research *objectives*, not research *questions*; (4) Prioritize verification and validation (V&V) in methodology sections -- structure_architect_agent should include dedicated V&V subsections;

## peer-review (7 agents)

| Agent | File | Role | Model |
|-------|------|------|-------|
| eic_agent | peer-review/agents/eic_agent.md | Triage, reviewer assignment, decision synthesis | opus |
| methodology_reviewer_agent | peer-review/agents/methodology_reviewer_agent.md | Methods validity + reproducibility assessment | opus |
| domain_reviewer_agent | peer-review/agents/domain_reviewer_agent.md | Domain-specific accuracy + contribution evaluation | opus |
| perspective_reviewer_agent | peer-review/agents/perspective_reviewer_agent.md | Framing, bias, alternative interpretation review | opus |
| devils_advocate_reviewer_agent | peer-review/agents/devils_advocate_reviewer_agent.md | Adversarial critique + assumption stress-testing | opus |
| field_analyst_agent | peer-review/agents/field_analyst_agent.md | Field positioning + novelty + impact assessment | sonnet |
| editorial_synthesizer_agent | peer-review/agents/editorial_synthesizer_agent.md | Cross-review synthesis + actionable revision plan | opus |

> **Computational Mechanics / Materials Science Override:** When the user's field is computational mechanics or computational materials science, all reviewer agents should: (1) Use Pattern 7 (Computational/Modeling) as the default evaluation framework; (2) Default to numbered citations in feedback; (3) Evaluate research *objectives* rather than research *questions*; (4) Prioritize V&V assessment -- methodology_reviewer_agent should check for verification (convergence studies, code validation) and validation (comparison with experiments) as primary criteria;

## full-workflow (3 agents)

| Agent | File | Role | Model |
|-------|------|------|-------|
| pipeline_orchestrator_agent | full-workflow/agents/pipeline_orchestrator_agent.md | Stage detection, dispatch, state management | sonnet |
| integrity_verification_agent | full-workflow/agents/integrity_verification_agent.md | Reference/citation/data verification | sonnet |
| state_tracker_agent | full-workflow/agents/state_tracker_agent.md | Pipeline state tracking + checkpoint management | haiku |

> **Computational Mechanics / Materials Science Override:** When the user's field is computational mechanics or computational materials science, the pipeline orchestrator should: (1) Default all downstream skills to Pattern 7 (Computational/Modeling) structure; (2) Default to numbered citations throughout the pipeline; (3) Frame all scoping prompts around research *objectives*, not research *questions*; (4) Inject V&V checkpoints at methodology and review stages;

---

## Model Routing

### Tier Definitions

| Tier | Model | Use For | Cost (relative) |
|------|-------|---------|-----------------|
| **opus** | claude-opus-4-6 | Deep reasoning, synthesis, adversarial critique, quality judgment, nuanced writing | 1.0x (baseline) |
| **sonnet** | claude-sonnet-4-6 | Structured work, checklists, search, formatting, compliance checks, literature screening | ~0.2x |
| **haiku** | claude-haiku-4-5 | Simple triage, metadata extraction, state tracking, mechanical format conversion | ~0.04x |

### Distribution: 15 Opus / 18 Sonnet / 2 Haiku

### Override Policy

- Default tiers are **advisory, not enforced**. The user can override any agent's model.
- To override, pass `--model <tier>` when launching a subprocess or specify in the pipeline config.
- If a Sonnet agent produces inadequate output (malformed, shallow, or missing key reasoning), **escalate to Opus for that agent only** — do not upgrade the entire pipeline.
- **Never silently upgrade to Opus.** Always log the escalation reason in the stage manifest.
- Downgrades are permitted when the task is simpler than expected (e.g., formatter_agent on plain Markdown → stays Haiku).

### Cost Context

- A full pipeline run defaults to ~200K input + 100K output tokens.
- Opus agents (synthesis, drafting, review) consume ~112K of that budget — these are the high-value tasks where Opus quality matters.
- Routing the remaining 88K through Sonnet/Haiku saves ~35% on model costs.
- Combined with prompt caching, compressed screening, parallel verification, and session continuity (see `token_architecture.md`), estimated savings: **~45-52%**.

### Subprocess Model Passing

When launching agents as subprocesses (e.g., reviewer isolation via `claude --print`), pass the model flag:

```bash
claude --model <tier> --print -p "You are {agent_role}. ..."
```

The orchestrator reads the Model column from this registry to determine the correct tier for each subprocess.

### Escalation Notes

- `formatter_agent` (sonnet): Default is Sonnet due to complex LaTeX/APA 7 rules. **Downgrade to Haiku** only for plain Markdown or simple format conversions with no LaTeX.
- `monitoring_agent` (haiku): Sufficient for progress tracking; escalate only if anomaly detection logic is needed.
- `state_tracker_agent` (haiku): Mechanical checkpoint work; no escalation expected.

---

## Loading Rules

1. **Load this registry** at pipeline start. Keep in context throughout.
2. **Load agent cards** (Tier 2) only when their phase begins.
3. **Never load more than 3 agent definitions simultaneously.**
4. **Release agent cards** when their phase completes.
5. **Escalate to Tier 3** (full .md) only if Tier 2 card is insufficient.
