# Agentic Research Assistant

[![License: CC BY-NC 4.0](https://img.shields.io/badge/license-CC%20BY--NC%204.0-lightgrey)](https://creativecommons.org/licenses/by-nc/4.0/)

A multi-agent workflow for academic research — literature review, paper writing, peer review, and full research-to-submission pipelines — all inside Claude Code.

> **AI is your copilot, not the pilot.** This tool handles the structured work — searching literature, formatting citations, verifying references, checking consistency — so you can focus on defining the question, choosing the method, interpreting results, and making the argument.

---

## What It Does

**4 skills you can trigger by just asking:**

| Trigger | Skill | What happens |
|---------|-------|-------------|
| "research [topic]" | `literature-review` | Systematic web-based search, source verification, cross-source synthesis, gap analysis |
| "write a paper on [topic]" | `paper-writing` | Intake → outline → draft → cite → format, section by section |
| "review this paper" | `peer-review` | Multiple isolated analytical perspectives + editorial synthesis |
| "full pipeline" | `full-workflow` | Chains all three with integrity checks and checkpoints at every stage |

### Full Pipeline (11 stages)

```
literature-review (socratic/full)
  → paper-writing (plan/full)
    → integrity check (pre-review)
      → peer-review (full/guided)
        → human review gate
          → paper-writing (revision)
            → peer-review (re-review)
              → integrity check (final)
                → finalize (MD + DOCX + LaTeX → PDF)
                  → process summary
```

Every stage requires user confirmation. Integrity gates cannot be bypassed.

---

## Key Features

- **Citation verification** — every reference is metadata-checked via DOI resolution + WebSearch spot-check. Catches hallucinated citations. Terminal verdicts only: VERIFIED, NOT_FOUND, MISMATCH (plus non-blocking flags for paywalled/vague sources)
- **Isolated review perspectives** — multiple analytical perspectives run in separate subprocesses so they can't see each other's output. Prevents anchoring bias. (These are structured self-review frames from the same model, not independent human reviewers.)
- **V&V as first-class criterion** — for computational mechanics papers, verification (mesh convergence, MMS, code validation) and validation (comparison with experiments) are primary review criteria
- **Figure analysis** — methodology reviewer can visually evaluate convergence plots, stress contours, and damage localizations
- **Style calibration** — drop your previous papers in and it learns your writing voice. Applied as a soft guide; discipline and journal conventions always override
- **Cost-optimized** — only tasks requiring deep reasoning use the expensive model. Structured work runs on lighter models. ~45-52% cheaper than running everything on Opus

### Capability Boundaries (be honest about what this is)

| Capability | Status |
|------------|--------|
| Literature search | Web-based only; no direct access to paywalled databases |
| Citation verification | Metadata checks only; cannot verify in-text accuracy |
| Peer review | Structured self-review from multiple perspectives; not independent human reviewers |
| Paper output | Structured draft requiring human review before submission |
| Domain expertise | Pattern-matched from training data; no lived research experience |

---

## Installation

### As Project Skills (recommended)

```bash
cd /path/to/your/project
mkdir -p .claude/skills
git clone https://github.com/vprithiv/agentic-research-assistant .claude/skills/agentic-research-assistant
```

Then start Claude Code in your project:

```bash
claude
```

Skills auto-load when relevant to your conversation.

### As a Standalone Project

```bash
git clone https://github.com/vprithiv/agentic-research-assistant
cd agentic-research-assistant
claude
```

### Prerequisites

- [Claude Code](https://claude.ai/install) installed
- Anthropic API key ([get one here](https://console.anthropic.com/))
- Recommended model: Claude Opus 4.6 with Max plan (full pipeline consumes 200K+ tokens)

---

## Usage

```
# Literature review
"Research the impact of [topic] on [field]"

# Paper writing
"Write a paper on [topic]"

# Guided modes (Socratic dialogue)
"Guide my research on [topic]"
"Guide me through writing a paper on [topic]"

# Peer review
"Review this paper" (then provide the paper)

# Full pipeline
"I want to write a complete research paper on [topic]"

# Check pipeline status
"status"
```

### Supported Citation Formats

APA 7.0 (default), Chicago, MLA, IEEE, Vancouver

### Supported Paper Structures

IMRaD, Literature Review, Theoretical, Case Study, Policy Brief, Conference, Computational/Modeling

---

## Computational Mechanics / Materials Science

When your field is computational mechanics or materials science, the system automatically:

- Uses the Computational/Modeling paper structure
- Defaults to numbered citations (not APA author-date)
- Asks for research *objectives* instead of research *questions*
- Adds V&V checkpoints (mesh convergence, MMS, experimental validation)
- Reviews for computational fallacies (mesh-dependent localization, volumetric locking, hourglass modes, thermodynamic inconsistency, boundary condition artifacts)

---

## Style Calibration

Drop 2-3 of your previous papers into a conversation and say:

> "Calibrate a style profile from these papers"

The system analyzes your sentence length, vocabulary, citation patterns, and register shifts, then applies your voice as a soft guide when drafting. Discipline and journal conventions always take priority.

See `shared/style_profiles/` for an example profile and the schema.

---

## Cost Optimization

The system routes each agent to the appropriate model tier:

| Tier | Used for | Agents |
|------|----------|--------|
| **Opus** (15) | Synthesis, drafting, adversarial critique, quality judgment | synthesis, draft_writer, all reviewers, editorial_synthesizer |
| **Sonnet** (18) | Search, compliance, formatting, orchestration | bibliography, citation_compliance, formatter, orchestrator |
| **Haiku** (2) | State tracking, monitoring | state_tracker, monitoring |

Additional optimizations: two-tier compressed literature screening, batched reference verification, cross-phase research session persistence, prompt caching.

Combined estimated savings: **~45-52%** vs running all agents on Opus.

---

## License

This work is licensed under [CC-BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/).

---

## Acknowledgment

This project was originally derived from [academic-research-skills](https://github.com/Imbad0202/academic-research-skills) by Cheng-I Wu. It has since been substantially redesigned — including skill renaming, cost optimization with model routing, working set architecture, batched verification, figure analysis, multi-review integrity checks, and computational mechanics specialization.
