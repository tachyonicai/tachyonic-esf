# Specification Versioning

The ESF specification follows [Semantic Versioning](https://semver.org/) adapted for framework specifications.

## Version Format: MAJOR.MINOR.PATCH

**MAJOR** — Breaking changes to the framework structure. Examples: adding or removing a phase, fundamentally changing the maturity scoring system, restructuring the phase dependency model. Systems assessed under a previous major version may need re-assessment.

**MINOR** — Backward-compatible additions. Examples: new worked examples, new bridging concepts, additional decision criteria, new framework mappings, expanded glossary entries. Existing assessments remain valid.

**PATCH** — Corrections and clarifications. Examples: fixing typos, clarifying ambiguous definitions, correcting anti-pattern descriptions. No impact on assessments.

## Pre-release Suffixes

- `-draft` — Under active development, not yet reviewed
- `-rc.N` — Release candidate N, under community review
- No suffix — Released and stable

## Status Tags in the Specification

Each section carries a status tag:

- `[STABLE]` — Well-defined, unlikely to change structurally across minor versions
- `[DRAFT]` — Substantive but may evolve in minor versions
- `[PLACEHOLDER]` — Reserved for future expansion
- `[EXAMPLE NEEDED]` — Content gap to be filled

## File Naming

Specification files are named `ESF-v{VERSION}.md`. Only the current version is active. Previous versions are retained for reference but clearly marked as superseded.
