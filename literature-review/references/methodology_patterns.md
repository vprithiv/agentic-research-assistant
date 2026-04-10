# Research Methodology Patterns — Design Templates

## Purpose
Ready-to-use methodology templates for common research designs. Used by the research_architect_agent.

## Pattern 1: Systematic Literature Review

### When to Use
- Mapping the state of knowledge on a topic
- Identifying gaps in existing research
- Synthesizing evidence for policy/practice recommendations

### Design Template
```
Research Question: What is known about [topic] in [context]?

Protocol:
1. Register protocol (PROSPERO or similar)
2. Define search strategy (databases, keywords, Boolean operators)
3. Establish inclusion/exclusion criteria
4. Search execution + documentation
5. Two-pass screening (title/abstract → full text)
6. Quality appraisal of included studies
7. Data extraction
8. Synthesis (narrative, thematic, or meta-analytic)
9. Report per PRISMA guidelines

Quality Criteria:
- Comprehensive search (minimum 3 databases)
- Reproducible strategy
- Dual screening (2 reviewers or reviewer + verification)
- PRISMA checklist completed

Reporting Standard: PRISMA 2020 (see references/equator_reporting_guidelines.md)
```

### PRISMA Flow Template
```
Records identified through database searching (n = )
Additional records from other sources (n = )
         ↓
Records after duplicates removed (n = )
         ↓
Records screened (title/abstract) (n = )
Records excluded (n = )
         ↓
Full-text articles assessed for eligibility (n = )
Full-text excluded, with reasons (n = )
         ↓
Studies included in synthesis (n = )
```

## Pattern 2: Comparative Case Study

### When to Use
- Comparing policies, programs, or institutions
- Understanding how context shapes outcomes
- Generating theoretical propositions from multiple cases

### Design Template
```
Research Question: How does [phenomenon] vary across [cases]?

Protocol:
1. Case selection (theoretical or purposive sampling)
2. Define comparison framework (dimensions, variables)
3. Data collection per case (documents, interviews, data)
4. Within-case analysis
5. Cross-case analysis
6. Pattern identification and explanation

Quality Criteria:
- Explicit case selection rationale
- Consistent data collection across cases
- Both within-case and cross-case analysis
- Rival explanations considered
```

### Comparison Matrix Template
```
| Dimension | Case A | Case B | Case C | Pattern |
|-----------|--------|--------|--------|---------|
| Context   |        |        |        |         |
| Input     |        |        |        |         |
| Process   |        |        |        |         |
| Outcome   |        |        |        |         |
```

## Pattern 3: Policy Analysis

### When to Use
- Evaluating existing or proposed policies
- Comparing policy approaches across jurisdictions
- Assessing policy outcomes and unintended consequences

### Design Template
```
Research Question: How effective is [policy] in achieving [goal]?

Framework Options:
A. Bardach's Eightfold Path
B. Dunn's Policy Analysis Framework
C. SWOT Analysis
D. Logic Model (Input → Activity → Output → Outcome → Impact)

Protocol:
1. Problem definition
2. Evidence gathering (quantitative + qualitative)
3. Policy option identification
4. Criteria development (effectiveness, efficiency, equity, feasibility)
5. Option assessment against criteria
6. Recommendation with trade-offs

Quality Criteria:
- Multiple criteria (not just effectiveness)
- Stakeholder perspectives included
- Unintended consequences assessed
- Implementation feasibility addressed
```

## Pattern 4: Mixed Methods (Convergent Parallel)

### When to Use
- Complex phenomena requiring multiple data types
- Need to triangulate findings
- Quantitative data needs qualitative explanation (or vice versa)

### Design Template
```
Research Question: What is the nature and extent of [phenomenon]?

Protocol:
QUAN strand:                    QUAL strand:
1. Survey/data collection       1. Interviews/focus groups
2. Statistical analysis         2. Thematic analysis
3. Quantitative findings        3. Qualitative findings
                    ↓
            4. Integration
            5. Joint display
            6. Meta-inference

Quality Criteria:
- Both strands have independent rigor
- Integration strategy explicit (not just parallel reporting)
- Joint display or mixed methods matrix
- Meta-inferences draw on both strands

Reporting Standards: QUAL strand → COREQ; QUAN strand → STROBE/CONSORT (see references/equator_reporting_guidelines.md)
```

## Pattern 5: Content/Document Analysis

### When to Use
- Analyzing texts, policies, media, or documents
- Identifying patterns in communication
- Systematic examination of large document sets

### Design Template
```
Research Question: What themes/patterns emerge from [document set]?

Protocol:
1. Define corpus (which documents, inclusion criteria)
2. Develop coding framework (deductive, inductive, or hybrid)
3. Code systematically (inter-coder reliability if multiple coders)
4. Analyze codes → categories → themes
5. Report with exemplar quotes/excerpts

Quality Criteria:
- Corpus selection transparent
- Coding framework documented
- Inter-coder reliability reported (if applicable)
- Saturation discussed
```

## Pattern 6: Exploratory Research

### When to Use
- New or under-researched topics
- Generating hypotheses for future research
- Understanding phenomena from participant perspective

### Design Template
```
Research Question: How do [participants] experience/understand [phenomenon]?

Protocol:
1. Purposive sampling
2. Semi-structured interviews or observations
3. Iterative data collection and analysis
4. Open coding → axial coding → selective coding
5. Theory or framework development
6. Member checking / peer debriefing

Quality Criteria:
- Reflexivity statement
- Thick description
- Data saturation discussed
- Transferability criteria addressed

Reporting Standard: COREQ for interviews/focus groups (see references/equator_reporting_guidelines.md)
```

## Pattern 7: Benchmarking Study

### When to Use
- Comparing performance against standards or peers
- Identifying best practices
- Setting performance targets

### Design Template
```
Research Question: How does [entity] perform compared to [benchmark]?

Protocol:
1. Select benchmarking type (internal, competitive, functional, generic)
2. Identify indicators and metrics
3. Collect comparable data
4. Analyze gaps
5. Identify best practices from high performers
6. Develop improvement recommendations

Quality Criteria:
- Comparable metrics (apples to apples)
- Context factors acknowledged
- Multiple indicators (not single metric)
- Actionable recommendations
```

## Pattern 8: Technology Requirements Analysis

### When to Use
- Assessing feasibility, requirements analysis, and technology comparison for new technologies
- Technology selection decisions before system design
- Risk and benefit assessment of technology adoption
- When research questions involve "Which technology should be used?" or "Can this technology solve the problem?"

### Design Template
```
Research Question: What technology approach best addresses [need] given [constraints]?

Protocol:
1. Requirement Elicitation
   - Stakeholder interviews
   - Existing system/process analysis
   - Functional requirements vs non-functional requirements (performance, security, scalability)
2. Technology Scanning
   - Inventory of candidate technologies (at least 3 options)
   - Technology Readiness Level (TRL) assessment
   - Community activity, documentation completeness, long-term maintenance risk
3. Feasibility Assessment
   - Technical feasibility: Can it be done?
   - Economic feasibility: Is it worth doing?
   - Organizational feasibility: Does the team have the capability?
   - Schedule feasibility: Is there enough time?
4. Proof of Concept (PoC)
   - Construct minimal verification targeting key technical risks
   - Define success criteria (performance thresholds, integration test pass rates)
   - Document encountered problems and solutions
5. Requirement Specification
   - Produce formal requirements document
   - Define acceptance criteria
   - Establish traceability matrix (requirements ↔ design ↔ testing)

Quality Criteria:
- Requirements completeness: All stakeholder requirements have been collected
- Traceability: Each requirement is traceable to its source; each design decision maps to a corresponding requirement
- Technical feasibility verification: Key technical risks have been validated through PoC
- Fair comparison of options: Consistent evaluation framework used to compare different technology options
```

### Technology Comparison Matrix Template
```
| Evaluation Dimension | Option A | Option B | Option C | Weight |
|---------------------|----------|----------|----------|--------|
| Functional Fit      |          |          |          | 30%    |
| Technology Maturity  |          |          |          | 20%    |
| Adoption Cost        |          |          |          | 15%    |
| Maintenance Cost     |          |          |          | 10%    |
| Learning Curve       |          |          |          | 10%    |
| Scalability          |          |          |          | 10%    |
| Community/Ecosystem  |          |          |          | 5%     |
| Weighted Total       |          |          |          | 100%   |
```

## Pattern 9: Legal Case Analysis

### When to Use
- Legal and regulatory policy analysis, case law research, legal text interpretation
- Analyzing current regulations and judicial opinions on specific legal issues
- Comparing legal approaches across different jurisdictions
- When research questions involve statutory interpretation, rights and obligations analysis, or legal aspects of policy analysis

### Distinction from Pattern 3 (Policy Analysis)
- **Policy Analysis**: Focuses on evaluating policy effectiveness — "Is this policy working?" "Are there better policy options?"
- **Legal Case Analysis**: Focuses on analyzing legal texts and case law — "What does the law say?" "How do courts interpret it?" "Are there legal loopholes?"

### Design Template
```
Research Question: How does the law address [issue] and what are the implications for [context]?

Protocol:
1. Issue Identification
   - Translate research question into specific legal issues
   - Distinguish questions of fact vs questions of law
   - Define the relevant legal domains (public law / private law / international law)
2. Legal Framework Mapping
   - Constitutional-level provisions
   - Statutory / regulatory / administrative rule levels
   - International conventions / soft law
   - Legislative history and rationale for amendments
3. Case Law Analysis
   - Systematic case law search (court level, time range, keywords)
   - Extract key holdings from decisions
   - Analyze trends in case law evolution
   - Identify majority opinions vs dissenting opinions
4. Legal Reasoning
   - Textual interpretation, systematic interpretation, purposive interpretation, historical interpretation
   - Comparative law analysis (how other jurisdictions handle the issue)
   - Review and evaluate scholarly opinions
   - Interest balancing and value judgments
5. Recommendations
   - Interpretive recommendations under existing law
   - Legislative reform recommendations (if necessary)
   - Practical implementation recommendations
   - Risk warnings

Quality Criteria:
- Legal source accuracy: Cited regulations and cases must be current and effective versions
- Logical consistency: Legal reasoning process must not be self-contradictory
- Argumentation completeness: All possible interpretive paths have been considered
- Comparative law rigor: When comparing jurisdictions, differences in legal system backgrounds must be noted
```

### Legal Analysis Structure Template
```
I. Legal Issues
   [Specific legal issues in dispute]

II. Relevant Provisions
   1. Statutory level:
   2. Regulatory level:
   3. International norms:

III. Judicial Opinions
   1. Majority opinion: [Case number] [Key holding]
   2. Dissenting opinion: [Case number] [Key holding]
   3. Trends:

IV. Scholarly Opinions
   1. View A:
   2. View B:
   3. Author's view:

V. Comparative Law
   [How other jurisdictions handle the issue]

VI. Conclusions and Recommendations
```

## Pattern 10: Creative/Practice-Based Research

### When to Use
- Art-based research: Generating knowledge through artistic creation
- Design research / research through design: Generating knowledge through the design process
- Practice-based / practice-led research: Practice itself is the research method
- When research questions involve creative practice, design thinking, or artistic inquiry

### Differences from Traditional Academic Research
- **Output format**: Can be a creative work + dissertation (not just a dissertation)
- **Knowledge type**: Values practical knowledge (tacit knowledge) and embodied knowledge
- **Process as method**: The creative/design process itself is the research method, not merely the object of study
- **Subjectivity**: The researcher's subjective experience is a legitimate source of knowledge, but requires systematic reflection

### Design Template
```
Research Question: What knowledge emerges through the practice of [creative activity] in [context]?

Protocol:
1. Reflective Practice
   - Define research question and creative intention
   - Establish reflective framework (e.g., Schön's reflection-in-action / reflection-on-action)
   - Confirm researcher positioning (insider / practitioner-researcher)
2. Process Documentation
   - Studio journal / design diary
   - Process video/audio documentation
   - Iteration version records (sketches, drafts, prototypes)
   - Decision point documentation: Why this approach and not another?
3. Contextual Analysis
   - Situate the creative process within disciplinary/cultural/historical context
   - Engage in dialogue with existing works/theories
   - Identify themes and insights emerging from the creative process
4. Knowledge Articulation
   - Transform tacit knowledge into communicable forms
   - Build bridges from practice to concepts
   - Distill transferable principles or frameworks
5. Presentation of Findings
   - Work presentation (exhibition, performance, prototype demonstration)
   - Written discourse (exegesis / critical commentary)
   - Integrate the relationship between work and discourse

Quality Criteria:
- Depth of reflection: Not just describing "what was done," but analyzing "why it was done this way" and "what was learned"
- Creative process transparency: Readers can understand the complete path from problem to work
- Clarity of knowledge contribution: Clearly state what this research contributes to knowledge
- Contextualization quality: The work does not exist in isolation but engages with the discipline
- Methodological reflexivity: The researcher is aware of their own role and biases
```

### Practice-Based Research Documentation Template
```
Phase 1: Positioning
- Research question:
- Creative intention:
- Researcher positioning (practitioner / observer / participant):
- Theoretical framework:

Phase 2: Process
| Iteration | Date | Action | Reflection | Turning Point |
|-----------|------|--------|------------|---------------|
| v1        |      |        |            |               |
| v2        |      |        |            |               |
| v3        |      |        |            |               |

Phase 3: Outcomes
- Work description:
- Knowledge contribution:
- Transferable principles/frameworks:
- Recommendations for future practice/research:
```

## Pattern 11: Continuum-Scale Simulation Study (FEM/FVM/FDM)

### When to Use
- Crystal plasticity, phase-field, fracture mechanics, fluid mechanics, heat transfer
- Component-scale or mesoscale problems governed by PDEs
- When experimental parametric studies are too costly or dangerous

### Design Template
```
Research Question: How does [physical phenomenon] behave under [conditions] in [material/system]?

Protocol:
1. Design
   - Mesh convergence study
   - Boundary condition specification
   - Constitutive model selection
2. Implementation
   - Code/solver selection (commercial vs open-source)
   - Discretization scheme
   - Time integration method
3. Verification
   - Method of Manufactured Solutions (MMS)
   - Patch tests
   - Analytical benchmarks
   - Convergence rate verification (spatial and temporal)
4. Validation
   - Comparison with experiments
   - Error quantification (L2 norm, pointwise, etc.)
5. Application
   - Parametric studies
   - Predictions beyond experimental range

Quality Criteria:
- Mesh convergence demonstrated
- Convergence rates match theoretical expectations
- Validation against independent experimental data
- Uncertainty in input parameters acknowledged
```

## Pattern 12: Atomistic Simulation Study (MD/MC)

### When to Use
- Grain boundary studies, diffusion, defect energetics, phase transformations
- Nanoscale phenomena where continuum assumptions break down
- Property calculation from atomic interactions

### Design Template
```
Research Question: What are the [properties/mechanisms] of [material/defect] at the atomic scale?

Protocol:
1. Design
   - Interatomic potential selection and benchmarking
   - Ensemble choice (NVE, NVT, NPT, etc.)
   - System size convergence study
2. Implementation
   - Equilibration protocol
   - Production runs
   - Timestep convergence verification
3. Analysis
   - Statistical mechanics post-processing
   - Error estimation (block averaging, autocorrelation)
4. Validation
   - Comparison to experimental properties (lattice parameter, elastic constants, etc.)

Quality Criteria:
- Potential benchmarked against target properties
- System size effects quantified
- Statistical errors reported
- Equilibration verified (energy, pressure convergence)
```

## Pattern 13: First-Principles Study (DFT/ab initio)

### When to Use
- Electronic structure, defect formation energies, elastic constants, surface energies
- When empirical potentials are unavailable or insufficiently accurate
- Reference data generation for lower-scale models

### Design Template
```
Research Question: What are the [electronic/energetic/structural] properties of [material/defect/surface]?

Protocol:
1. Design
   - Functional selection (LDA/GGA/hybrid/meta-GGA)
   - Pseudopotential selection
   - k-point convergence testing
2. Implementation
   - Energy cutoff convergence testing
   - k-mesh convergence testing
   - Structural relaxation (forces, stresses)
3. Analysis
   - Electronic structure (band structure, DOS)
   - Energetics (formation energies, reaction energies)
   - Property calculation (elastic, dielectric, etc.)
4. Validation
   - Comparison to experimental measurements
   - Comparison to higher-level theory where available

Quality Criteria:
- Convergence with respect to cutoff energy and k-points demonstrated
- Functional choice justified for the property of interest
- Known DFT limitations acknowledged (band gap, van der Waals, strongly correlated)
- Spin polarization and magnetic effects considered where relevant
```

## Pattern 14: Multi-Scale Computational Study

### When to Use
- Integrated computational materials engineering (ICME), materials by design
- Problems where phenomena at one scale govern behavior at another
- When no single-scale method captures all relevant physics

### Design Template
```
Research Question: How do [lower-scale phenomena] influence [higher-scale behavior] in [material/system]?

Protocol:
1. Design
   - Scale identification (which scales are relevant)
   - Information passing strategy (parameters, constitutive laws, boundary conditions)
   - Homogenization approach (computational, analytical)
2. Implementation
   - Scale bridging: sequential vs concurrent coupling
   - Parameter passing protocol
   - Consistency checks across scales
3. Verification & Validation
   - Verification at each scale independently
   - Cross-scale validation
   - End-to-end validation against macroscopic experiments

Quality Criteria:
- Each scale independently verified
- Information loss at scale transitions quantified
- Cross-scale consistency demonstrated
- Overall predictions validated against experiments
```

## Pattern 15: Parametric / Sensitivity Study

### When to Use
- Uncertainty quantification, model calibration, design optimization
- Identifying which input parameters most influence outputs
- Exploring design spaces efficiently

### Design Template
```
Research Question: How sensitive is [output/response] to [input parameters] in [model/system]?

Protocol:
1. Design
   - Design of Experiments: factorial, Latin hypercube, Sobol sequences
   - Parameter space definition (ranges, distributions)
   - Response quantity selection
2. Implementation
   - Sampling strategy execution
   - Surrogate model construction (Gaussian process, polynomial chaos, neural network)
   - Convergence of sensitivity indices
3. Analysis
   - Sensitivity indices (Sobol first-order, total-order)
   - Main effects and interaction effects
   - Response surface visualization

Quality Criteria:
- Sufficient samples for convergence of sensitivity indices
- Parameter ranges justified from physical constraints or literature
- Surrogate model accuracy validated (cross-validation, held-out data)
- Results interpreted in physical terms, not just statistical
```

## Choosing the Right Pattern

```
What type of question?
├── "What is known?" → Systematic Literature Review
├── "How do cases compare?" → Comparative Case Study
├── "Is this policy working?" → Policy Analysis
├── "What's happening and why?" → Mixed Methods
├── "What do documents reveal?" → Content Analysis
├── "How is this experienced?" → Exploratory Research
├── "How do we compare?" → Benchmarking Study
├── "Which technology should we use?" → Technology Requirements Analysis
├── "What does the law say?" → Legal Case Analysis
├── "What knowledge emerges from practice?" → Creative/Practice-Based Research
├── "How does this system behave (continuum PDE)?" → Continuum-Scale Simulation Study
├── "What happens at the atomic scale?" → Atomistic Simulation Study
├── "What are the electronic/energetic properties?" → First-Principles Study
├── "How do scales connect?" → Multi-Scale Computational Study
└── "Which parameters matter most?" → Parametric / Sensitivity Study

More nuanced decision:
├── Technology assessment related
│   ├── Comparing different technology options → Pattern 8 (Technology Requirements Analysis)
│   └── Comparing technology adoption across organizations → Pattern 2 (Comparative Case Study)
├── Law/policy related
│   ├── What legal texts prescribe and how courts interpret them → Pattern 9 (Legal Case Analysis)
│   └── Whether a policy is effective and how to improve it → Pattern 3 (Policy Analysis)
├── Creative/design related
│   ├── Generating knowledge through the creative process → Pattern 10 (Creative/Practice-Based Research)
│   ├── Understanding the experience of creators → Pattern 6 (Exploratory Research)
│   └── Analyzing creative texts/works → Pattern 5 (Content Analysis)
├── Computational science related
│   ├── Solving PDEs at continuum scale → Pattern 11 (Continuum-Scale Simulation Study)
│   ├── Nanoscale atomic interactions → Pattern 12 (Atomistic Simulation Study)
│   ├── Electronic structure / quantum mechanics → Pattern 13 (First-Principles Study)
│   ├── Bridging multiple length/time scales → Pattern 14 (Multi-Scale Computational Study)
│   └── Parameter importance / uncertainty → Pattern 15 (Parametric / Sensitivity Study)
└── Uncertain
    ├── New topic with scarce literature → Pattern 6 (Exploratory Research)
    ├── Complex problem requiring multiple data types → Pattern 4 (Mixed Methods)
    └── First see how others have approached it → Pattern 1 (Systematic Literature Review)
```
