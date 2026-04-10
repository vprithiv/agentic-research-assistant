# Academic Writing Style Guide

Used by `draft_writer_agent` and `peer_reviewer_agent`.

## Core Principles

### 1. Precision
- Use the most specific term available
- Define technical terms on first use
- Avoid ambiguous pronouns ("this," "it") without clear antecedents

### 2. Conciseness
- Eliminate filler words and redundant phrases
- One idea per sentence (or clearly connected ideas)
- Prefer short sentences for complex ideas

### 3. Objectivity
- Base claims on evidence, not opinion
- Use hedging for uncertain claims
- Acknowledge limitations and alternative interpretations

### 4. Formality
- No contractions (don't → do not)
- No colloquialisms or slang
- No first person unless discipline conventions allow it

## Register Adjustment by Discipline

### Sciences (Natural, Applied)
```
Register: Formal, impersonal, method-focused
Voice: Passive voice common ("was measured," "were analyzed")
Terminology: Precise measurements, SI units, statistical notation
Example: "The sample was heated to 350°C for 2 hours, yielding a conversion rate of 87.3% (SD = 2.1)."
```

### Social Sciences
```
Register: Formal, theory-informed, participant-aware
Voice: Active voice encouraged, first person for researcher decisions
Terminology: Theoretical constructs, operationalized variables
Example: "We employed semi-structured interviews to explore how participants understood institutional change (N = 24)."
```

### Humanities
```
Register: Formal, argument-driven, interpretive
Voice: First person acceptable for arguments, active voice
Terminology: Close reading vocabulary, theoretical language
Example: "I argue that the text's spatial metaphors reveal an underlying anxiety about institutional permanence."
```

### Engineering / CS
```
Register: Formal, problem-solution oriented, specification-precise
Voice: Passive common for methods, active for contributions
Terminology: Technical specifications, performance metrics
Example: "The proposed algorithm achieves O(n log n) complexity, outperforming the baseline by 34% on the benchmark dataset."
```

### Education
```
Register: Formal, practice-oriented, stakeholder-aware
Voice: Active voice, first person for reflexive practice
Terminology: Pedagogical concepts, assessment language
Example: "The intervention improved student metacognitive awareness, as evidenced by a significant increase in self-regulation scores (t(45) = 3.21, p = .002, d = 0.72)."
```

### Medicine / Health
```
Register: Formal, evidence-hierarchy conscious, clinical precision
Voice: Passive for methods, active for findings
Terminology: Clinical terms, diagnostic criteria, statistical reporting
Example: "Patients receiving the intervention showed a 40% reduction in readmission rates (RR = 0.60, 95% CI [0.45, 0.80], p = .001)."
```

## Hedging and Strength Language

### Hedging (for uncertain or qualified claims)
| Strength | Hedging Devices | Example |
|----------|----------------|---------|
| Weak | may, might, could, possibly | "This may suggest a correlation." |
| Moderate | suggests, indicates, appears | "The data suggest a positive trend." |
| Strong | demonstrates, establishes, confirms | "The evidence demonstrates a clear link." |

### When to Hedge
- Results that need replication
- Causal claims from correlational data
- Generalizations from limited samples
- Interpretations with alternative explanations

### When NOT to Hedge
- Reporting factual data: "The response rate was 78%." (not "appeared to be")
- Describing methodology: "We used thematic analysis." (not "we attempted to use")
- Well-established facts: "Earth orbits the Sun." (not "may orbit")

## Transition Words and Phrases

### Addition
moreover, furthermore, in addition, additionally, similarly, likewise

### Contrast
however, nevertheless, in contrast, on the other hand, conversely, whereas

### Cause/Effect
therefore, consequently, as a result, thus, hence, accordingly

### Example
for example, for instance, specifically, in particular, such as, namely

### Sequence
first, second, third, subsequently, finally, meanwhile

### Summary
in summary, to conclude, overall, taken together, in short

### Concession
although, despite, while, granted that, notwithstanding

## Paragraph Construction

### Standard Academic Paragraph (TEEL)
1. **T**opic sentence — states the paragraph's main point
2. **E**vidence — data, citations, examples that support the point
3. **E**xplanation — interpret the evidence, connect to argument
4. **L**ink — connect to the next paragraph or back to thesis

### Example
> **[T]** AI-assisted quality assurance has shown promise in improving evaluation consistency across institutions. **[E]** Smith (2024) found that institutions using AI tools reported a 23% reduction in inter-rater variance, while Chen and Wang (2023) documented improved agreement on scoring rubrics (κ = 0.82 vs. 0.64). **[E]** These findings suggest that algorithmic assistance can mitigate the subjective biases inherent in human evaluation, particularly when assessors have varying levels of experience. **[L]** However, the reliance on AI tools also raises concerns about the loss of contextual judgment, which the following section addresses.

## Common Style Errors

### Wordiness
| Wordy | Concise |
|-------|---------|
| in order to | to |
| due to the fact that | because |
| a large number of | many |
| at the present time | currently / now |
| it is important to note that | notably |
| in the event that | if |
| has the ability to | can |
| with regard to | regarding / about |
| in spite of the fact that | despite / although |
| conduct an investigation of | investigate |

### Vague Language
| Vague | Precise |
|-------|---------|
| "many studies" | "several studies (e.g., Chen, 2023; Smith, 2024)" |
| "a significant impact" | "a 23% increase in retention rates" |
| "in recent years" | "since 2020" or "over the past five years" |
| "some researchers" | Name them with citations |
| "it is well known that" | Cite the source or remove |

### Tense Usage
| Section | Tense | Example |
|---------|-------|---------|
| Literature review (reporting findings) | Past | "Smith (2024) found that..." |
| Literature review (ongoing state) | Present | "The theory posits that..." |
| Methodology | Past | "Data were collected through..." |
| Results | Past | "The analysis revealed..." |
| Discussion (interpreting) | Present | "These findings suggest..." |
| Conclusion (implications) | Present/Future | "This has implications for... / Future research should..." |

## Computational Mechanics / Materials Science Conventions

### Equation-Prose Integration
- Equations are part of the sentence: they follow a colon or lead-in phrase and may end with a comma or period
- Introduce every equation before displaying it: "The balance of linear momentum reads" or "The constitutive relation is given by"
- After each displayed equation, include a "where" clause defining all newly introduced symbols
- Short expressions may remain inline (e.g., "the von Mises stress *σ*_vm = √(3*J*₂)") if they do not break readability
- Multi-step derivations use aligned environments; number only the key results that are referenced later
- Never present an equation without connecting it to the surrounding argument

### Notation Standards
- **Vectors**: bold lowercase — **u**, **v**, **n**, **t**
- **Tensors / Matrices**: bold uppercase — **F**, **C**, **σ**, **P**
- **Scalars**: italic — *E*, *ν*, *ρ*, *T*, *p*
- Greek letters for material/constitutive parameters (*μ*, *λ*, *κ*, *ν*); Latin letters for geometric and kinematic quantities (*L*, *A*, *u*, *x*)
- Subscript conventions:
  - Italic subscripts for tensor indices: *σ*_{*ij*}, *C*_{*ijkl*}
  - Roman (upright) subscripts for labels: *σ*_y (yield), *K*_IC (fracture toughness), **F**^p (plastic)
- Maintain a consistent symbol table throughout the paper; include a nomenclature section if the journal supports it
- Never reuse a symbol for two different quantities

### Unit Formatting
- Use SI units throughout unless the target journal specifies otherwise
- Units in upright (roman) font, not italic: "MPa" not "*MPa*"
- Always include a space between the number and the unit: "200 MPa" not "200MPa"
- Use negative exponents rather than division for compound units: "kg m⁻³" not "kg/m³" (or use the journal's convention)
- Temperature: "350 °C" or "623 K" — note the space before the degree symbol for Celsius
- Dimensionless quantities: state explicitly (e.g., "the Poisson ratio *ν* = 0.3 (dimensionless)")

### Mathematical Writing Conventions
- Define every symbol at its first occurrence in the text
- Never start a sentence with a mathematical symbol; rephrase: "The stress *σ* exceeds..." not "*σ* exceeds..."
- Use "where" clauses immediately after displayed equations to define all new notation
- Distinguish clearly between a definition (≡ or :=) and an equation (=)
- Use consistent notation for common operations: ∇ for gradient, div for divergence, ":" for double contraction
- Write ranges with an en-dash: "elements 1–100", "Eqs. (3)–(7)"

### Figure Conventions for Engineering
- Abbreviate as "Fig. 1" mid-sentence; spell out "Figure 1" at the start of a sentence
- Every figure must be referenced in the text before it appears
- Contour plots: always include a colorbar with units; state deformation scale factor if the mesh is shown in deformed configuration
- Stress-strain or force-displacement curves: label both axes with quantity and unit (e.g., "Stress [MPa]", "Strain [-]"); include a legend with descriptive condition labels
- Convergence plots: use log-log axes where appropriate; annotate the observed convergence rate
- Mesh figures: state total element count, element type (e.g., "8-node hexahedra"), and characteristic element size

### Table Conventions for Engineering
- Tables always referenced as "Table 1" (never abbreviated)
- Parameter / material property tables should include columns for: Symbol, Description, Value, Unit, Source/Reference
- Convergence study tables should include columns for: Mesh (or DOFs), Element Size, Result, Error (%), Convergence Rate
- Use horizontal rules to separate header from body; avoid vertical rules (per most journal style guides)
- Numerical values aligned on the decimal point where possible
- Include units in the column header, not repeated in every cell: "Stress [MPa]" in the header, then just "250" in the cell
