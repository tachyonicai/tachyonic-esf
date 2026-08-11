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

Map the ESF to additional industry standards or frameworks. Current mappings:

| File | Framework | Pinned at |
|---|---|---|
| `owasp-llm-top10.yaml` | OWASP GenAI LLM Top 10 | 2026 v1.0 |
| `owasp-agentic-top10.yaml` | OWASP Top 10 for Agentic Applications (ASI) | 2026 |
| `mitre-atlas.yaml` | MITRE ATLAS (tactic level) | 2026.07 |
| `aarm.yaml` | CSA AARM | R1-R9 |

We welcome mappings to:

- NIST AI Risk Management Framework (AI RMF) and NIST AI 600-1
- ISO/IEC 27001 (especially Annex A controls) and ISO/IEC 42001
- CSA AI Controls Matrix (AICM)
- STRIDE threat modeling
- Google SAIF
- MITRE ATLAS at technique level — the existing mapping covers the 16 tactics only, and the pinned release carries 101 top-level techniques and 77 sub-techniques

Submit as YAML in `mappings/` following the existing schema, or open an issue using the "Framework Extension" template to discuss first.

#### Mapping conventions

Upstream frameworks move, and several now move monthly. Mappings must be pinned and must fail loudly when they go stale:

- **`framework_version` is required.** State what release the mapping was written against. Where the upstream publishes no version number, pin by requirement set and retrieval date.
- **Add `framework_pin` where the upstream is a repository.** A commit SHA is better than a tag and much better than "latest".
- **Record identifier migrations.** Where an upstream rebinds identifiers between releases, carry the old one — `previous_id` in the OWASP mappings — so a reader can tell a moved identifier from a wrong one. The 2026 OWASP release rebound eight of ten identifiers while adding and removing no risks; a mapping keyed on the identifier alone failed silently rather than obviously.
- **Do not invent taxonomy IDs.** Where an upstream's scope now exceeds what `tachyonic-sh/taxonomy` covers, record the gap in `notes` rather than filling it with an ID that does not exist.
- **Verify against the pin, not against the website.** Framework sites render the current release; the pinned artifact is what the mapping claims to describe.

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
