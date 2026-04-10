# Style Profiles

Pre-computed author writing style profiles for the paper-writing skill. These profiles allow the drafting pipeline to match an author's natural voice without requiring fresh writing samples each time.

## Quick Start (New Users)

Drop 2-3 of your previous papers into a conversation and say:

> "Calibrate a style profile from these papers"

The profile will be saved here and automatically applied when drafting. Discipline and journal conventions always take priority — your style is applied as a soft guide (Priority 3).

## Location

Profiles are stored as Markdown files in this directory (`style_profiles/`) and mirrored in `shared/style_profiles/` for cross-skill access. Each file is named `{authorname}.md` (lowercase, no spaces).

A copy is also maintained in `shared/style_profiles/` so that consumers in other skills (e.g., `literature-review/agents/report_compiler_agent`) can reference them without path gymnastics.

## How Profiles Are Selected

Selection happens at **intake_agent Step 10**:

| Scenario | Behavior |
|----------|----------|
| 1 profile exists | Auto-load with confirmation prompt |
| Multiple profiles | Present list, user picks one |
| No profiles exist | Fall back to sample-based calibration |
| User says "skip" | `style_profile: null`, no style applied |
| User says "new" | Run calibration from fresh samples |

## Schema

Each profile must contain the **Schema 10 required fields** (see `shared/handoff_schemas.md` Schema 10):

| Field | Type | Required |
|-------|------|----------|
| `calibration_source` | list[string] | Yes |
| `sample_count` | integer | Yes |
| `sentence_length` | object (`mean`, `stddev`, `rhythm_pattern`) | Yes |
| `paragraph_length` | object (`mean_sentences`, `variation`) | Yes |
| `vocabulary_preferences` | object (`hedging_words`, `transition_words`, `preferred_verbs`, `formality`) | Yes |
| `citation_style` | object (`narrative_ratio`, `parenthetical_ratio`, `density`, `placement`) | Yes |
| `modifier_style` | enum (`minimal` / `moderate` / `elaborate`) | Yes |
| `register_shifts` | list of `{section_name, assertiveness_level}` | Yes |

### Extended Fields (Optional)

These capture patterns that don't map onto the 6 core dimensions:

| Field | Description |
|-------|-------------|
| `information_flow` | Within-paragraph sequencing (claim → mechanism → evidence → implication) |
| `section_scaffolding` | Section-level structural patterns (intro funnels, results ordering) |
| `cross_section_bridging` | Forward/backward references, transitional openers, figure interpretation |
| `complexity_handling` | How multi-factor analyses are presented (one-at-a-time vs. interleaved) |
| `distinctive_traits` | Signature patterns (roadmap paragraphs, abstract structure, punctuation habits) |

Extended fields are consumed as **Priority 3 (SOFT)** guidance — same level as the core style dimensions. See `shared/style_calibration_protocol.md` for the full priority hierarchy.

## Creating a New Profile

### Option A: Automatic calibration (recommended)

1. During intake (Step 10), provide 3+ writing samples when prompted
2. The intake agent runs calibration per `shared/style_calibration_protocol.md`
3. Save the resulting profile to `style_profiles/{authorname}.md`

### Option B: Manual authoring

1. Copy an existing profile as a template
2. Fill in all Schema 10 required fields
3. Add extended fields as needed
4. Save as `style_profiles/{authorname}.md`
5. Copy to `shared/style_profiles/{authorname}.md`

## Updating Profiles

Profiles can be updated as an author's style evolves. When updating:
- Add new samples to `calibration_source`
- Update `sample_count`
- Revise dimensions that have shifted
- Note any evolution in the profile's Notes section
