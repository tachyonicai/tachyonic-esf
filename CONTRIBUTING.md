# Contributing to the Evolutionary Security Framework

Thank you for your interest in contributing to the ESF. This framework improves through practitioner feedback, real-world application, and community expertise.

## Ways to Contribute

### Worked Examples (high impact)

Trace a specific security property or threat through all ten ESF phases. Good candidates include:

- A specific attack vector (e.g., indirect prompt injection via RAG poisoning)
- A security property of a real system (e.g., "no agent can escalate privileges without human authorization")
- A defense mechanism evolving through the phases (e.g., from heuristic rate-limiting to formally verified resource bounds)

Submit as a markdown file in `examples/worked-examples/` following the existing format.

### Framework Mappings

Map the ESF to additional industry standards or frameworks. Current mappings cover OWASP LLM Top 10 and OWASP Agentic Top 10. We welcome mappings to:

- NIST AI Risk Management Framework (AI RMF)
- ISO/IEC 27001 (especially Annex A controls)
- MITRE ATLAS (expanding the existing mapping)
- STRIDE threat modeling
- Google SAIF

Submit as YAML in `mappings/` following the existing schema.

### Assessment Feedback

If you apply the ESF rubric to a real system, we'd value feedback on:

- Were the scoring criteria clear and unambiguous?
- Did the maturity profiles match your system's actual shape?
- What gaps did the assessment reveal that the framework doesn't address?

Open an issue using the "Phase Feedback" template.

### Phase Refinements

Improve definitions, decision criteria, anti-patterns, or core concepts based on practitioner experience. Changes to the specification require:

1. An issue describing the proposed change and rationale
2. A PR against the spec in `spec/`
3. Review by at least one maintainer

## Guidelines

- **Practitioner-first language** — write for security engineers, not philosophers. If a concept needs a technical term, define it on first use.
- **Evidence-based** — support claims with references, real-world examples, or data where possible.
- **Implementation-agnostic** — the framework describes epistemological phases, not technology choices. Avoid language-specific or tool-specific guidance in the spec. Implementation details belong in `examples/`.
- **Respect the open/private boundary** — the ESF is an open framework. Do not include proprietary detection logic, payloads, scoring algorithms, or other competitive IP in contributions.

## Process

1. **Issues first** — for non-trivial changes, open an issue to discuss before writing a PR
2. **One concern per PR** — keep PRs focused on a single change or addition
3. **Spec changes are versioned** — modifications to `spec/ESF-v*.md` will be batched into versioned releases

## Code of Conduct

We follow the [Contributor Covenant](https://www.contributor-covenant.org/version/2/1/code_of_conduct/). Be respectful, constructive, and inclusive.

## Questions?

Open an issue or reach out at security@tachyonicai.com.
