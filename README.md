# Evolutionary Security Framework (ESF)

**A maturity model for progressively hardening agentic AI security systems — from naming threats to mathematically proving defenses.**

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Version](https://img.shields.io/badge/spec-v0.1.0--draft-orange.svg)](/spec/ESF-v0.1.0.md)

---

## The Problem

Most AI security is stuck in two modes: **ad-hoc heuristics** ("block anything that says 'ignore previous instructions'") or **compliance checklists** ("we address OWASP LLM Top 10"). Neither tells you *how to mature* — how to take an imperfect defense and progressively harden it until it's provably correct.

The result: security teams know *what* to worry about but not *how to systematically get better*.

## The Framework

The ESF defines **ten phases** that describe how security knowledge matures — from unstructured observation to mathematical proof. Each phase converts uncertainty into structure.

```
Name → Relate → Guess → Measure → Model → Explain → Formalize → Constrain → Prove → Evolve
```

| Phase | Verb | Question | You go from → to |
|:-----:|------|----------|-------------------|
| 1 | **Name** | What exists? | Chaos → Categories |
| 2 | **Relate** | How does it connect? | Categories → Structure |
| 3 | **Guess** | What might go wrong? | Structure → Intuition |
| 4 | **Measure** | Does it actually work? | Intuition → Evidence |
| 5 | **Model** | What patterns emerge? | Evidence → Prediction |
| 6 | **Explain** | Why does it happen? | Prediction → Understanding |
| 7 | **Formalize** | What's always true? | Understanding → Rules |
| 8 | **Constrain** | What's impossible? | Rules → Architecture |
| 9 | **Prove** | Can we guarantee it? | Architecture → Certainty |
| 10 | **Evolve** | What's next? | Certainty → New Questions |

**The key insight:** not everything moves to Phase 9. The distribution is intentionally pyramidal — many heuristics, few proofs. The framework helps you decide *what to harden* based on consequence, stability, frequency, and trust boundary position.

## How It Relates to OWASP

The ESF is **complementary to OWASP**, not competitive.

- **OWASP LLM Top 10** tells you *what* the risks are
- **OWASP Agentic Top 10** tells you *what's different* about agentic AI systems
- **ESF** tells you *how to progressively harden* against those risks — from first detection to formal proof

The ESF [maps directly to both OWASP frameworks](/mappings/) so you can assess your maturity against risks you already track.

## Quick Start

**Assess your system in 30 minutes:**

1. Read the [ten-phase overview](/spec/ESF-v0.1.0.md#3-the-ten-phases-stable) (5 min)
2. Score your system using the [assessment scorecard](/rubric/assessment-scorecard.yaml) (20 min)
3. Identify your gaps and prioritize using the [maturity profiles](/rubric/maturity-profiles.yaml) (5 min)

**Go deeper:**

- Full specification → [`spec/ESF-v0.1.0.md`](/spec/ESF-v0.1.0.md)
- Map your own system → [`mappings/pipeline-mapping-template.yaml`](/mappings/pipeline-mapping-template.yaml)
- See a real-world mapping → [`examples/tachyonic-pipeline-mapping.md`](/examples/tachyonic-pipeline-mapping.md)

## Repository Structure

```
tachyonic-esf/
├── spec/
│   └── ESF-v0.1.0.md                 # The living specification
├── rubric/
│   ├── assessment-scorecard.yaml      # Machine-readable scoring criteria
│   ├── maturity-profiles.yaml         # Common system archetypes
│   └── gap-analysis-template.yaml     # Gap prioritization matrix
├── guides/
│   └── quick-start.md                 # Assess your system in 30 minutes
├── mappings/
│   ├── owasp-llm-top10.yaml          # ESF ↔ OWASP LLM Top 10
│   ├── owasp-agentic-top10.yaml       # ESF ↔ OWASP Agentic Top 10
│   └── pipeline-mapping-template.yaml # Map YOUR system to ESF
└── examples/
    ├── tachyonic-pipeline-mapping.md  # Reference implementation
    └── worked-examples/               # Single threats traced through all 10 phases
```

## Core Principles

**Progressive Determinism** — Move security properties from low determinism (heuristics) to high determinism (formal proof), at the appropriate pace for each property's consequence and maturity.

**The Funnel** — Many things at Phase 1-3, fewer at 4-5, fewer still at 6-7, only the most critical at 8-9. Phase 10 applies to everything. Not all threats need formal verification — most shouldn't.

**Cyclical Maturation** — The framework is a spiral, not a waterfall. Phase 10 feeds back into Phase 1 at a higher baseline. Known threats get pushed deeper into determinism. New threats enter at Phase 1.

**Self-Application** — The framework applies to itself. A system built on ESF should be assessed by ESF — including its own attack surface and evolution mechanisms.

## Reference Implementation

The ESF is grounded in two concrete artifacts:

**[tachyonic-heuristics](https://github.com/tachyonicai/tachyonic-heuristics)** — An open taxonomy of 122 AI/LLM attack vectors mapped to OWASP LLM Top 10 and MITRE ATLAS. Implements ESF Phases 1-3 (taxonomy, ontology, heuristics). Apache 2.0.

**The Tachyonic Security Pipeline** — An agentic 11-stage security research pipeline that implements Phases 3-10 operationally. The pipeline accepts targets, runs methodology, self-improves with each campaign, and demonstrates the full ESF cycle in production. See the [pipeline mapping](/examples/tachyonic-pipeline-mapping.md) for details.

## Maturity Assessment

The ESF includes a [scoring rubric](/rubric/assessment-scorecard.yaml) that rates each phase 0-4:

| Score | Level | Definition |
|:-----:|-------|-----------|
| 0 | Absent | Phase not addressed |
| 1 | Ad-hoc | Informal, undocumented |
| 2 | Defined | Formally defined, not yet measured |
| 3 | Measured | Instrumented, quantitatively tracked |
| 4 | Optimizing | Continuously measured and actively improving |

Common maturity profiles:

| Profile | Shape | Typical System |
|---------|-------|----------------|
| **Reactive** | Low everywhere, Phase 3 highest | Ad-hoc guardrails, no measurement |
| **Operational** | Strong 1-5, weak 6-9 | Good detection, no formal guarantees |
| **Hardened** | Strong 1-4 and 7-8, weak 5-6 | Rules exist but aren't causally grounded |
| **Research-grade** | Strong 1-6, weak 7-9 | Deep understanding, limited enforcement |
| **Mature** | Strong across all, Phase 9 selective | Full spectrum, verification applied selectively |

## Who This Is For

- **Security engineers** building defenses for AI/LLM/agentic systems — use the framework to identify gaps and prioritize hardening
- **Security architects** designing trust boundaries — use Phase 8 (Constrain) and Phase 9 (Prove) as design targets
- **Red teams** assessing AI systems — use the taxonomy (Phase 1) and attack chains (Phase 2) as coverage checklists
- **Engineering leaders** evaluating security maturity — use the rubric to score systems and track improvement
- **Researchers** studying AI security — use the framework as an organizing structure for threat analysis and defense evaluation

## Contributing

We welcome contributions across the framework. See [CONTRIBUTING.md](/CONTRIBUTING.md) for guidelines.

High-value contributions:
- **Worked examples** — trace a specific threat (prompt injection, data exfiltration, privilege escalation) through all ten phases
- **Framework mappings** — map ESF to additional standards (NIST AI RMF, ISO 27001, STRIDE)
- **Assessment feedback** — apply the rubric to a real system and share what worked or didn't
- **Phase refinements** — improve definitions, decision criteria, or anti-patterns based on practitioner experience

## Professional Assessment

Want your AI system assessed against the full ESF? [Tachyonic](https://tachyonicai.com) runs 48-hour security assessments that test against all 144 attack vectors with full reporting, resistance scoring, and ESF maturity assessment.

[Book a scoping call →](https://cal.com/tachyonicai/ai-security-scoping)

## License

Apache 2.0 — see [LICENSE](/LICENSE).

## Citation

```
@misc{tachyonic-esf,
  title={Evolutionary Security Framework: A Maturity Model for Progressive Determinism in Agentic Security Systems},
  author={Tachyonic},
  year={2026},
  url={https://github.com/tachyonicai/tachyonic-esf}
}
```
