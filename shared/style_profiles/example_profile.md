# Style Profile: Example Author

**Profile Version**: 1.0
**Created**: 2026-04-07
**Last Updated**: 2026-04-07

> This is an anonymized example profile. To create your own, drop 2-3 of your previous papers into a conversation and say "Calibrate a style profile from these papers."

---

## Schema 10 — Required Fields

**Calibration Source**: ["Author_2020_materials_fatigue.pdf", "Author_2022_microstructure_analysis.pdf", "Author_2024_computational_mechanics.pdf"]
**Sample Count**: 3

**Sentence Length**:
- mean: 28
- stddev: 12
- rhythm_pattern: "long-dominant — routinely 30+ words with multi-clause structures; short sentences (< 15 words) rare, reserved for transitions or definitions"

**Paragraph Length**:
- mean_sentences: 6
- variation: "long and substantive — literature-review paragraphs can exceed 10 sentences; Methods paragraphs slightly shorter (4-6); single-paragraph lit-review sweeps are common"

**Vocabulary Preferences**:
- hedging_words: ["could potentially", "may result in", "is likely to", "is expected to", "appears to"]
- transition_words: ["Furthermore", "Additionally", "Moreover", "However", "Hence", "To this end", "Therefore"]
- preferred_verbs: ["conducted", "characterized", "investigated", "employed", "utilized", "addressed"]
- formality: "high-formal — no colloquial language, humor, or rhetorical flourish; deliberate understatement when results are favorable"

**Citation Style**:
- narrative_ratio: 0.45
- parenthetical_ratio: 0.55
- density: 2.5 per paragraph
- placement: "literature-review sections use narrative-heavy '[Author] et al.' sequential surveys; results/discussion use parenthetical for supporting evidence"

**Modifier Style**: moderate

**Register Shifts**:
- section_name: "Introduction" | assertiveness_level: "measured — contextual, building toward gap"
- section_name: "Methods" | assertiveness_level: "neutral-procedural — passive voice dominant"
- section_name: "Results" | assertiveness_level: "descriptive — trend-value-interpretation triplets"
- section_name: "Discussion" | assertiveness_level: "restrained-assertive — strong claims for well-supported findings, immediate pivot to caveats"
- section_name: "Conclusion" | assertiveness_level: "summary-mode — enumerated key findings or flowing prose"

---

## Extended Fields

### Information Flow (within-paragraph sequencing)

- **Dominant structure**: Motivation-first
- **Typical progression**: Contextual/motivational statement → method/analysis description → result or implication
- **Literature review pattern**: Long single-paragraph passages surveying multiple studies sequentially, building toward a gap statement
- **Gap statement form**: "However, [what is missing]. [This work / the present study] addresses this gap by..."
- **Caveat placement**: Consistently at the end after main claim/result is stated
- **Overall pattern**: Assertion → Evidence → Qualification

### Section Scaffolding

- **Introductions**: Broad context → thematic lit review (general → specific) → gap identification → objectives → roadmap paragraph
- **Methods**: Bottom-up (geometry/material → model → simulation details)
- **Results**: Simple → complex; deliberate escalation of complexity
- **Discussion**: Restate findings → contextualize → limitations → future directions

### Distinctive Traits

- **Roadmap paragraphs**: Previews structure section-by-section
- **Long structured abstracts**: 150-250 words; problem-method-results-significance structure
- **Em dash usage**: Extensively used for parenthetical insertions
- **Passive voice dominance**: Active voice primarily with "this work"/"this study" as subject
- **Limitation transparency**: Thorough acknowledgment of model limitations in dedicated paragraphs

---

## Notes

- This is an example profile for a computational mechanics / materials science author
- Replace with your own calibrated profile by providing 3+ writing samples during intake
- See `shared/style_calibration_protocol.md` for the full calibration process
