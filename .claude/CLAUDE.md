# Academic Research Skills

A suite of Claude Code skills for systematic academic research, paper writing, structured self-review, and pipeline orchestration.

## Skills Overview

| Skill | Purpose | Key Modes |
|-------|---------|-----------|
| `literature-review` v2.4 | Universal 13-agent research team | full, quick, socratic, review, lit-review, fact-check, systematic-review |
| `paper-writing` v2.5 | 12-agent academic paper writing | full, plan, outline-only, revision, abstract-only, lit-review, format-convert, citation-check, revision-coach, pre-submit |
| `peer-review` v1.4 | Multi-perspective paper review (5 reviewers) | full, re-review, quick, methodology-focus, guided |
| `full-workflow` v3.0 | Full pipeline orchestrator | (coordinates all above) |

## Routing Rules

1. **full-workflow vs individual skills**: full-workflow = full pipeline orchestrator (research → write → review → revise → finalize). If the user only needs a single function (just research, just write, just review), trigger the corresponding skill directly without the pipeline.

2. **literature-review vs paper-writing**: Complementary. literature-review = upstream research engine (investigation + fact-checking), paper-writing = downstream publication engine (paper writing + English abstracts). Recommended flow: literature-review → paper-writing.

3. **literature-review socratic vs full**: socratic = guided Socratic dialogue to help users clarify their research question. full = direct production of research report. When the user's research question is unclear, suggest socratic mode.

4. **paper-writing plan vs full**: plan = chapter-by-chapter guided planning via Socratic dialogue. full = direct paper production. When the user wants to think through their paper structure, suggest plan mode.

5. **peer-review guided vs full**: guided = Socratic review that engages the author in dialogue about issues. full = standard multi-perspective review report. When the user wants to learn from the review, suggest guided mode.

## Key Rules

- All claims must have citations
- Evidence hierarchy respected (meta-analyses > RCTs > cohort > case reports > expert opinion)
- Contradictions disclosed with evidence quality comparison
- AI disclosure in all reports
- Output language: English

## Full Academic Pipeline

```
literature-review (socratic/full)
  → paper-writing (plan/full)
    → peer-review (full/guided)
      → paper-writing (revision)
        → peer-review (re-review, max 2 loops)
          → paper-writing (format-convert → final output)
```

## Handoff Protocol

### literature-review → paper-writing
Materials: RQ Brief, Methodology Blueprint, Annotated Bibliography, Synthesis Report, INSIGHT Collection

### paper-writing → peer-review
Materials: Complete paper text. field_analyst_agent auto-detects domain and configures reviewers.

### peer-review → paper-writing (revision)
Materials: Editorial Decision Letter, Revision Roadmap, Per-reviewer detailed comments

## Model Routing for Cost Optimization

Agents are assigned default model tiers to balance quality and API cost.

**Distribution: 15 Opus / 18 Sonnet / 2 Haiku**

| Tier | When to Use | Example Agents |
|------|------------|----------------|
| **Opus** (15) | Deep reasoning, synthesis, adversarial critique, nuanced writing | synthesis_agent, draft_writer_agent, all reviewers (eic, methodology, domain, perspective, devils_advocate), editorial_synthesizer_agent |
| **Sonnet** (18) | Structured work, checklists, search, formatting, compliance | research_question_agent, bibliography_agent, citation_compliance_agent, pipeline_orchestrator_agent |
| **Haiku** (2) | Simple triage, metadata, state tracking | monitoring_agent, state_tracker_agent |

**When to override:**
- **Upgrade** Sonnet → Opus: Agent output is shallow or misses key reasoning (e.g., structure_architect on a highly interdisciplinary paper)
- **Downgrade** Sonnet → Haiku: Simple formatting (e.g., formatter_agent on plain Markdown with no LaTeX)
- **Downgrade** Opus → Sonnet: Task is simpler than expected (e.g., peer_reviewer on a short abstract-only check)

See `shared/agent_registry.md` for the full per-agent Model column and routing details.

## Style Profile

When drafting or revising academic prose, check `shared/style_profiles/` for an author style profile. If one exists, apply it as a soft writing guide (Priority 3). Discipline and journal conventions always take priority. If no profile exists, skip style calibration or offer to create one from writing samples.

## Version Info
- **Version**: 3.0
- **Last Updated**: 2026-04-07
- **Author**: Cheng-I Wu
- **License**: CC-BY-NC 4.0
