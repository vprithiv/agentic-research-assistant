# Source Quality Hierarchy — Evidence Grading Framework

## Purpose
Systematic framework for grading evidence quality, used by the source_verification_agent and bibliography_agent.

## Evidence Pyramid (7 Levels)

```
         ╱╲
        ╱ I ╲        Systematic Reviews / Meta-Analyses
       ╱──────╲
      ╱  II    ╲     Randomized Controlled Trials
     ╱──────────╲
    ╱   III      ╲   Controlled Studies (non-randomized)
   ╱──────────────╲
  ╱    IV          ╲  Case-Control / Cohort Studies
 ╱──────────────────╲
╱     V              ╲  Systematic Reviews of Descriptive Studies
╱──────────────────────╲
╱      VI                ╲  Single Descriptive / Qualitative Studies
╱──────────────────────────╲
╱       VII                  ╲  Expert Opinion / Committee Reports
╱──────────────────────────────╲
```

## Detailed Level Descriptions

### Level I: Systematic Reviews & Meta-Analyses
**Weight**: Highest
**Description**: Rigorous synthesis of all available evidence using predefined, systematic methods.
**Characteristics**:
- Pre-registered protocol (PROSPERO or similar)
- Comprehensive search across multiple databases
- Explicit inclusion/exclusion criteria
- Quality assessment of included studies
- Statistical pooling (meta-analysis) when appropriate
- PRISMA reporting guidelines followed

**Trusted Sources**: Cochrane Library, Campbell Collaboration, JBI Evidence Synthesis

**Caveats**: Quality depends on included studies ("garbage in, garbage out"); may be outdated if field moves fast.

### Level II: Randomized Controlled Trials (RCTs)
**Weight**: Very High
**Description**: Experimental studies with random allocation to intervention/control groups.
**Characteristics**:
- Random assignment
- Control/comparison group
- Blinding (single, double, or triple)
- Pre-registered protocol
- Adequate sample size
- Intention-to-treat analysis

**Caveats**: Not always feasible (especially in social science/education); ethical constraints; external validity concerns.

### Level III: Controlled Studies Without Randomization
**Weight**: High
**Description**: Quasi-experimental designs with comparison groups but no randomization.
**Characteristics**:
- Comparison group present
- Pre-post measurements
- Attempts to control confounds
- Larger samples than case studies

**Examples**: Difference-in-differences, propensity score matching, regression discontinuity.

**Caveats**: Selection bias risk; confounding variables harder to control.

### Level IV: Case-Control & Cohort Studies
**Weight**: Moderate-High
**Description**: Observational studies tracking groups over time or comparing cases to controls.
**Characteristics**:
- Longitudinal (cohort) or retrospective (case-control)
- Natural variation, no researcher intervention
- Large samples possible
- Real-world context

**Caveats**: Cannot establish causation; confounders possible; recall bias (case-control).

### Level V: Systematic Reviews of Descriptive/Qualitative Studies
**Weight**: Moderate
**Description**: Rigorous synthesis of qualitative or descriptive research.
**Characteristics**:
- Systematic search and selection
- Quality appraisal of included studies
- Meta-synthesis or meta-ethnography techniques
- Transparent methods

**Caveats**: Quality limited by included studies; interpretive layer adds subjectivity.

### Level VI: Single Descriptive or Qualitative Studies
**Weight**: Low-Moderate
**Description**: Individual case studies, ethnographies, surveys, descriptive analyses.
**Characteristics**:
- In-depth, context-rich
- Exploratory or descriptive purpose
- Small samples typical
- Thick description

**Caveats**: Limited generalizability; researcher subjectivity; no causal claims warranted.

### Level VII: Expert Opinion & Committee Reports
**Weight**: Lowest
**Description**: Position papers, editorials, committee reports, guidelines based on expert consensus.
**Characteristics**:
- Based on expertise and experience
- Often integrates multiple evidence types informally
- May reflect institutional or ideological positions

**Caveats**: Not empirically tested; potential bias; "authority" ≠ "evidence."

## Grading Rubric

### Per-Source Assessment

| Criterion | Grade A (Excellent) | Grade B (Good) | Grade C (Adequate) | Grade D (Weak) | Grade F (Unacceptable) |
|-----------|-------|-------|-------|-------|-------|
| Evidence Level | I-II | III | IV-V | VI | VII or unclassifiable |
| Peer Review | Rigorous peer review | Standard peer review | Editorial review | No formal review | Self-published |
| Methodology | Exemplary, replicable | Sound, described | Adequate | Questionable | Absent/flawed |
| Sample/Data | Large, representative | Adequate | Limited but justified | Small, convenience | Unspecified |
| Currency | < 3 years | 3-5 years | 5-10 years | > 10 years | Outdated for topic |
| Conflicts | None declared or detected | Minor, disclosed | Moderate, disclosed | Undisclosed potential | Clear undisclosed conflict |

### Overall Source Grade
- **A**: Use as primary evidence
- **B**: Use as supporting evidence
- **C**: Use with explicit caveats
- **D**: Use only if no better source; acknowledge weakness
- **F**: Do not use; cite only if critiquing

## Field-Specific Adjustments

Not all fields use the same evidence hierarchy. Adjust expectations:

| Field | Gold Standard | Common Level | Notes |
|-------|--------------|-------------|-------|
| Medicine/Health | Level I-II (RCTs, meta-analyses) | Level I-III | Evidence-based medicine tradition |
| Education | Level III-IV (quasi-experimental) | Level IV-VI | Randomization often impractical |
| Social Science | Level III-V | Level IV-VI | Mixed methods common |
| Policy | Level IV-V + VII (expert panels) | Level V-VII | Context-dependent; expert opinion valued |
| Humanities | Level VI (primary sources) | Level VI-VII | Different epistemology; "evidence" means different things |
| Technology | Level III + industry reports | Level V-VII | Fast-moving; peer review lags reality |

## Predatory Publication Indicators

### Red Flags Checklist
- [ ] Aggressive email solicitation to submit
- [ ] Acceptance within 72 hours of submission
- [ ] No identifiable editorial board (or fake names)
- [ ] Not indexed in Scopus, Web of Science, or PubMed
- [ ] Not member of COPE (Committee on Publication Ethics)
- [ ] Not listed in DOAJ (Directory of Open Access Journals)
- [ ] Excessively broad scope ("International Journal of Everything")
- [ ] Fake or inflated impact metrics
- [ ] Poor grammar/spelling on journal website
- [ ] APC (article processing charge) suspiciously low (< $200 for full OA)
- [ ] Editorial office in different country from stated location
- [ ] No retraction policy or ethics guidelines

### Verification Resources
- Beall's List (unofficial, but useful starting point)
- Cabell's Predatory Reports (subscription-based)
- DOAJ (whitelist of legitimate OA journals)
- COPE member directory
- Scopus Source List
- Journal Citation Reports (Clarivate)
- Think. Check. Submit. (thinkchecksubmit.org)

## Computational Science Source Hierarchy

### Evidence Hierarchy for Computational Studies

```
         ╱╲
        ╱ 1 ╲        Verified & validated simulation against multiple independent experiments
       ╱──────╲
      ╱   2    ╲     Simulation validated against single well-controlled experiment
     ╱──────────╲
    ╱    3       ╲   Simulation verified (convergence shown) but unvalidated
   ╱──────────────╲
  ╱     4          ╲  Benchmark problem reproduction (NIST, community challenges)
 ╱──────────────────╲
╱      5              ╲  Simulation with stated but unverified parameters
╱──────────────────────╲
╱       6                ╲  Simulation with no convergence study or validation
╱──────────────────────────╲
```

1. **Verified & validated against multiple independent experiments** (Highest): Simulation demonstrates mesh/timestep convergence AND matches multiple independent experimental datasets. Gold standard for computational science.
2. **Validated against single well-controlled experiment**: Convergence demonstrated and results compared to one experimental dataset with quantified error.
3. **Verified but unvalidated**: Convergence studies shown (mesh, timestep, iterative), but no experimental comparison. Common in methods papers.
4. **Benchmark problem reproduction**: Results compared to community benchmark problems (NIST, AFRL challenge problems) but not to new experimental data.
5. **Stated but unverified parameters**: Simulation parameters reported but no convergence study; relies on "standard" settings or prior work.
6. **No convergence study or validation** (Lowest): Black-box simulation with no verification or validation. Treat with extreme caution.

### Source Types Specific to Computational Science

| Source Type | Authority Level | Use For |
|-------------|----------------|---------|
| Code documentation (MOOSE, LAMMPS, VASP manuals) | Authoritative for implementation details | Solver capabilities, input syntax, algorithm descriptions |
| Benchmark databases (NIST, AFRL challenge problems) | Reference standard for V&V | Verification and validation targets |
| Interatomic potential repositories (OpenKIM, NIST IPR) | Primary source for atomistic parameters | Potential selection, property benchmarks, transferability data |
| Materials databases (Materials Project, AFLOW, ICSD) | Primary for DFT reference data | Crystal structures, formation energies, electronic properties |
| Technical reports (Sandia SAND, INL/EXT) | High — often contain critical methodology details | Implementation details, V&V procedures, convergence studies not in journal papers |
| Conference proceedings (WCCM, USNCCM, ECCOMAS) | Moderate — lower peer-review rigor | Early access to new methods, preliminary results |

### Field-Specific Currency Rules

| Category | Currency Window | Rationale |
|----------|----------------|-----------|
| Foundational methods (Cahn-Hilliard, finite elements, crystal plasticity) | No age limit — cite the original | These are established theoretical frameworks; the original derivation remains authoritative |
| Numerical implementations and codes | 5-10 year window | Codes evolve significantly; older versions may lack current features, bug fixes, or parallel capabilities |
| Applications and materials data | 5-year window | New experiments and higher-fidelity simulations supersede older results |
