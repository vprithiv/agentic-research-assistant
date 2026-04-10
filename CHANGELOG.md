# Changelog

All notable changes to this project will be documented in this file.

## [3.0] - 2026-04-07

### Removed
- **English-only conversion**: Removed all Chinese/Traditional Chinese (zh-TW) bilingual support
  - Deleted `abstract_bilingual_agent.md` → replaced with `abstract_agent.md` (English-only, 150-300 words, 5-component structure)
  - Deleted `README.zh-TW.md`, `chinese_paper_example.md`, `bilingual_abstract_template.md`, `apa7_chinese_citation_guide.md`
  - Deleted Chinese showcase PDFs (`full_paper_zh_apa7.pdf`, `paper_creation_process_zh.pdf`)
  - Removed Chinese trigger keywords from all SKILL.md files
  - Removed CJK font stacks (`xeCJK`, `setCJKmainfont`, `DFKai-SB`, `Noto CJK`) from formatter and LaTeX templates
  - Removed Chinese abstract guidelines, Chinese citation format sections, Chinese academic writing conventions
  - Removed Chinese format examples from funding and CRediT templates
  - Simplified Schema 4: `abstract` from `{english, chinese}` object to `string`; `keywords` from bilingual object to `list[string]`
  - Removed bilingual abstract mode references; `abstract-only` mode now produces English abstract only

## [2.8] - 2026-03-22

### Added
- **SCR Loop Phase 1** — State-Challenge-Reflect mechanism integrated into Socratic Mentor Agent
  - Commitment gates at layer/chapter transitions (collect user predictions before presenting evidence)
  - Certainty-triggered contradiction (probes high-confidence statements with counterpoints)
  - Adaptive intensity (tracks commitment accuracy, adjusts challenge frequency)
  - Self-calibration signal (S5) for convergence detection
  - SCR Switch — users can disable/re-enable predictions mid-dialogue
- `literature-review/agents/socratic_mentor_agent.md` — SCR Protocol section with commitment gates, divergence reveal, and adaptive intensity
- `literature-review/references/socratic_questioning_framework.md` — SCR Overlay Protocol mapping SCR phases to Socratic functions
- `paper-writing/agents/socratic_mentor_agent.md` — Chapter-level SCR Protocol with per-chapter commitment questions and cross-chapter pattern tracking

## [2.7.3] - 2026-03-10

### Fixed
- Version badge corrected in both EN and zh-TW READMEs

## [2.7.2] - 2026-03-10

### Added
- Version, license, and sponsor badges to README
- zh-TW README badges

## [2.7.1] - 2026-03-10

### Fixed
- Buy Me a Coffee username corrected

## [2.7] - 2026-03-09

### Added
- Integrity Verification v2.0: Anti-Hallucination Overhaul
- Full academic research skills suite (4 skills, 116 files)
- Deep Research v2.3 — 13-agent research team with 7 modes
- Academic Paper v2.4 — 12-agent paper writing with LaTeX hardening
- Academic Paper Reviewer v1.4 — Multi-perspective peer review with quality rubrics
- Academic Pipeline v2.6 — 10-stage orchestrator with integrity verification
