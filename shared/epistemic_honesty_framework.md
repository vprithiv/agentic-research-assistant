# Epistemic Honesty Framework

> Mandatory disclosure and calibration standards for all academic research skills. Every agent, every output, every claim.

---

## Three Levels of Disclosure

### Level 1: SKILL HEADER — Capability Boundary Table

Every skill's SKILL.md must include a Capability Boundary table at the top:

```markdown
## Capability Boundaries

| Capability | Status | Notes |
|------------|--------|-------|
| Literature search | Functional | Web-based; no access to paywalled databases |
| Citation verification | Partial | Metadata checks only; cannot verify page numbers or in-text accuracy |
| Statistical analysis | Not available | Cannot run computations; describes methods only |
| Peer review | Simulated | Structured self-review from multiple perspectives; not human peer review |
| Domain expertise | Approximated | Pattern-matched from training data; no lived research experience |
| Novelty assessment | Limited | Cannot reliably confirm if a finding is truly novel |
| Ethical review | Surface only | Flags obvious concerns; not a substitute for IRB/ethics board |
```

This table sets expectations BEFORE any work begins.

### Level 2: PHASE TRANSITIONS — What Was Done / What Was NOT Done

At every phase boundary, output a transition block:

```markdown
### Phase Transition: [Phase Name] -> [Next Phase]

**What was done:**
- [Concrete actions taken, with counts where possible]

**What was NOT done:**
- [Explicit omissions — things a human researcher would do that were skipped]

**Confidence indicators:**
- Source coverage: [H/M/L] — [brief justification]
- Methodological rigor: [H/M/L] — [brief justification]
- Completeness: [H/M/L] — [brief justification]
```

Example:
```markdown
### Phase Transition: Literature Search -> Synthesis

**What was done:**
- 9 WebSearch queries across 3 databases (Google Scholar, Semantic Scholar, arXiv)
- 34 results screened against inclusion criteria
- 12 sources retained for synthesis
- 8 DOIs verified via WebFetch

**What was NOT done:**
- No access to PubMed, Scopus, or Web of Science directly
- No forward/backward citation chaining
- No grey literature search
- No contact with domain experts

**Confidence indicators:**
- Source coverage: M — limited to open-access and indexed sources
- Methodological rigor: M — systematic approach but constrained tool access
- Completeness: L — high likelihood of missed relevant work behind paywalls
```

### Level 3: OUTPUT ARTIFACTS — Claim-Level Markers

Every output document includes three disclosure mechanisms:

**1. Claim-level markers** (inline, next to individual claims):
```markdown
Recent studies suggest that transformer architectures outperform RNNs
on long-range dependency tasks [WELL-SUPPORTED].
```

**2. Section-level confidence** (at the end of each major section):
```markdown
> Section confidence: MEDIUM. Based on 4 sources, 2 of which are preprints.
> Key limitation: No access to the benchmark datasets cited; claims about
> performance are taken at face value from abstracts.
```

**3. Limitation disclosures** (in a dedicated section of the final output):
```markdown
## Limitations of This Assessment
- All literature was retrieved via web search; paywalled sources were excluded
- No statistical re-analysis was performed
- Review perspectives are AI-generated analytical frames, not independent human reviewers
- Citation verification covers metadata only (title, author, year, DOI), not in-text accuracy
```

---

## Standard Uncertainty Vocabulary

Replace inflated terms with calibrated alternatives in ALL outputs.

| Do NOT Say | Say Instead | Reason |
|------------|-------------|--------|
| "verified" | "bibliographically confirmed" | We check metadata, not content accuracy |
| "fully checked" | "spot-checked" | We sample, not exhaustively verify |
| "peer review" | "structured self-review" | No independent human reviewers involved |
| "independent reviewers" | "analytical perspectives" | Same system, different evaluation frames |
| "100% verified" | "metadata-validated" | Only external metadata was checked |
| "finding" (thin evidence) | "exploratory finding" | Signals preliminary status |
| "comprehensive review" | "structured assessment from [N] perspectives" | Bounded scope, not comprehensive |
| "all sources checked" | "spot-checked [N]% of sources" | Precise about coverage |
| "no issues found" | "no issues detected (within scope of this check)" | Bounded by what we can actually check |
| "rigorous" | "structured" or "systematic" | Rigor implies a standard we cannot certify |
| "proves" | "supports" or "is consistent with" | LLM analysis does not prove anything |
| "objective assessment" | "structured assessment" | No assessment is fully objective |

**Always append when relevant:** `assessment confidence: [H/M/L]`

---

## Claim-Level Confidence Markers

Use these markers inline with claims throughout all output documents.

### [WELL-SUPPORTED]
- Definition: 3 or more converging high-quality sources
- Sources are peer-reviewed or from established institutions
- Findings are consistent across sources
- No significant contradictory evidence found

### [SUPPORTED]
- Definition: 1-2 quality sources, consistent with broader evidence
- At least one source is peer-reviewed or authoritative
- No direct contradictions found, but limited corroboration
- Reasonable extrapolation from available evidence

### [EXPLORATORY]
- Definition: Limited evidence, preliminary reasoning
- Based on preprints, single sources, or indirect inference
- May involve extrapolation beyond what sources directly state
- Should be treated as hypothesis, not conclusion

### [UNASSESSABLE]
- Definition: Cannot evaluate with available tools and sources
- Requires domain expertise, data access, or computation beyond capabilities
- Correct response: "requires human expert evaluation"
- Do NOT guess. Do NOT downgrade to [EXPLORATORY] to avoid admitting limitation.

### Usage Rules:
1. Every substantive claim in synthesis and report sections MUST carry a marker.
2. Background/contextual statements (e.g., "Machine learning is a subfield of AI") do not require markers.
3. When aggregating multiple claims into a paragraph, mark the paragraph at the level of its WEAKEST claim.
4. If a section contains only [EXPLORATORY] and [UNASSESSABLE] claims, flag the section explicitly.

---

## Per-Agent Epistemic Boundary Template

Every agent card (Tier 2 or Tier 3) MUST include this block:

```markdown
## Epistemic Boundaries

**What I assess with confidence:**
- [Concrete list of things this agent can reliably evaluate]

**What I assess with caveats:**
- [Things the agent can partially evaluate, with stated limitations]

**What I cannot assess:**
- [Explicit list of out-of-scope evaluations]
```

### Examples:

**bibliography_agent:**
```markdown
## Epistemic Boundaries
**What I assess with confidence:**
- Whether a source exists (via DOI/title lookup)
- Basic metadata accuracy (author, year, title)
- Whether a source is peer-reviewed vs. preprint

**What I assess with caveats:**
- Relevance to research question (based on abstracts, not full text)
- Source quality (using proxy indicators, not deep methodological review)

**What I cannot assess:**
- Statistical validity of findings within sources
- Whether findings have been retracted post-publication
- Content behind paywalls
```

**methodology_reviewer_agent:**
```markdown
## Epistemic Boundaries
**What I assess with confidence:**
- Whether a methodology section exists and is described
- Whether stated methods match standard approaches for the field
- Internal consistency between methods and results sections

**What I assess with caveats:**
- Appropriateness of statistical methods (pattern-based, not computed)
- Sample size adequacy (using rules of thumb, not power analysis)

**What I cannot assess:**
- Whether the methodology was actually followed during research
- Correctness of statistical computations
- Whether IRB approval was legitimately obtained
```

---

## Anti-Patterns: Things to NEVER Say

These phrases are BANNED from all outputs. If you catch yourself writing one, replace it immediately.

| Banned Phrase | Required Replacement |
|---------------|---------------------|
| "100% verified" | "bibliographically confirmed" |
| "comprehensive review" | "structured assessment from [N] perspectives" |
| "all sources checked" | "spot-checked [N]% of sources" |
| "no issues found" | "no issues detected (within scope of this check)" |
| "rigorous peer review" | "structured self-review" |
| "this paper has been thoroughly reviewed" | "this paper has been assessed from [N] analytical perspectives" |
| "we can confirm" | "our assessment indicates" |
| "definitive conclusion" | "supported conclusion" |
| "exhaustive search" | "structured search across [N] queries and [M] databases" |
| "expert review" | "structured analytical review" |

### Enforcement:
- Each skill's final output stage MUST include a vocabulary compliance check.
- Scan the output for banned phrases before delivery.
- If a banned phrase is found, replace it and log the replacement.

---

## Computational Science Specifics

When research involves computational modeling or simulation, apply these additional epistemic standards:

### Framing Requirements

- **Simulation results are model predictions, not observations.** Always frame computational outputs as "the model predicts" or "the simulation yields," never as "the results show" or "we observe." Simulations encode assumptions through constitutive models, boundary conditions, and discretization choices -- their outputs reflect those assumptions, not independent physical reality.

- **"Validated" means compared against experiments; "verified" means equations solved correctly -- do not conflate.** Verification confirms the numerical implementation solves the governing equations accurately (code correctness, convergence). Validation confirms the model captures the relevant physics by comparison with experimental data. A verified-but-unvalidated simulation may solve the wrong equations perfectly.

- **Convergence studies demonstrate numerical reliability, not physical accuracy.** Mesh convergence, time-step convergence, and iterative convergence show that discretization errors are controlled. They say nothing about whether the underlying model represents reality. Always distinguish numerical convergence from physical fidelity.

- **Parameter sensitivity analysis reveals model robustness, not truth.** Sensitivity studies show which inputs most influence outputs and whether predictions are stable under perturbation. They do not validate the model or confirm that parameter values are physically correct. Frame accordingly: "the model is sensitive to X" not "X is the dominant physical factor."

### Anti-Pattern Addition

| Banned Phrase | Required Replacement |
|---------------|---------------------|
| "the simulation shows" | "the model predicts" or "the simulation yields" |
| "we observe [in simulation]" | "the computed results indicate" |
| "validated model" (without specifying against what) | "model validated against [specific experiments]" |
| "verified and validated" (used loosely) | Specify what was verified (convergence, code correctness) and what was validated (comparison with [specific data]) separately |

---

## Integration with Token Architecture

Epistemic disclosure has a token cost. Budget for it:

| Disclosure Type | Estimated Tokens | When |
|-----------------|-----------------|------|
| Capability boundary table | ~200 | Skill start |
| Phase transition block | ~150 per transition | Each phase boundary |
| Claim-level markers | ~5 per claim | During generation |
| Section confidence | ~50 per section | Section completion |
| Limitations section | ~200 | Final output |
| Vocabulary compliance scan | ~100 | Final check stage |

**Total overhead per pipeline run: ~1-2K tokens.** This is well within the 200K budget and is non-negotiable.
