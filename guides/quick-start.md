# Quick Start: Assess Your System in 30 Minutes

This guide walks you through a rapid ESF maturity assessment. The goal isn't precision — it's identifying your biggest gaps so you know where to invest.

## Before You Start

You need:
- A basic understanding of your system's architecture (components, data flows, trust boundaries)
- Knowledge of what security controls are currently deployed
- 30 uninterrupted minutes

## Step 1: Score Each Phase (20 minutes)

For each of the ten phases, ask the core question and assign a score from 0-4. Use the criteria in [`rubric/assessment-scorecard.yaml`](/rubric/assessment-scorecard.yaml) for detailed guidance.

Work quickly — your first instinct is usually correct. You can refine later.

| Phase | Question | Your Score (0-4) |
|:-----:|----------|:-----------------:|
| 1 | Do we have a structured classification of threats, entities, and actions? | |
| 2 | Do we model how threats, components, and trust boundaries relate to each other? | |
| 3 | Do we have detection and response rules deployed, even if imperfect? | |
| 4 | Do we measure how well our detection rules actually perform? | |
| 5 | Do we use statistical models to detect patterns beyond hand-written rules? | |
| 6 | Do we understand *why* vulnerabilities exist — the root causes, not just symptoms? | |
| 7 | Do we have deterministic, formal rules that produce guaranteed correct answers? | |
| 8 | Are any security properties enforced by architecture rather than runtime checks? | |
| 9 | Are any critical properties mathematically verified across all possible states? | |
| 10 | Does the system systematically improve from each operational cycle? | |

## Step 2: Identify Your Profile (5 minutes)

Compare your scores to the profiles in [`rubric/maturity-profiles.yaml`](/rubric/maturity-profiles.yaml):

- **Reactive** — Low everywhere, Phase 3 highest. Ad-hoc guardrails, no measurement.
- **Operational** — Strong 1-5, weak 6-9. Good detection, limited understanding and enforcement.
- **Hardened** — Strong 1-4 and 7-8, weak 5-6. Rules exist but may not be causally grounded.
- **Research-grade** — Strong 1-6, weak 7-9. Deep understanding, limited enforcement.
- **Mature** — Strong across all, Phase 9 selective. Full spectrum with targeted formal verification.

Which profile most closely matches your system?

## Step 3: Prioritize (5 minutes)

The single most impactful next step depends on your profile:

| If you're... | Invest in... | Because... |
|---|---|---|
| Reactive | Phase 4 (Measure) | You can't improve what you don't measure |
| Operational | Phase 6 (Explain) | Move from detecting symptoms to eliminating causes |
| Hardened | Phase 6 (Explain) | Validate that rules are grounded in causal understanding |
| Research-grade | Phase 7 (Formalize) | Convert understanding into deterministic enforcement |
| Mature | Phase 9 (Prove) | Expand formal verification to additional critical properties |

## What's Next

- Read the full specification: [`spec/ESF-v0.1.0.md`](/spec/ESF-v0.1.0.md)
- Map your system's pipeline to ESF phases: [`mappings/pipeline-mapping-template.yaml`](/mappings/pipeline-mapping-template.yaml)
- See a reference mapping: [`examples/tachyonic-pipeline-mapping.md`](/examples/tachyonic-pipeline-mapping.md)
- Deep dive into OWASP mappings: [`mappings/owasp-llm-top10.yaml`](/mappings/owasp-llm-top10.yaml) and [`mappings/owasp-agentic-top10.yaml`](/mappings/owasp-agentic-top10.yaml)

## Common Questions

**Can I skip phases?**
In practice, yes — the phases describe a logical dependency chain, not a required execution sequence. But skipping Phase 6 (Explain) before Phase 7 (Formalize) means your formal rules may not be grounded in actual root causes.

**Does everything need to reach Phase 9?**
No. The funnel principle says most properties stay at Phases 1-3. Only the highest-consequence properties at critical trust boundaries justify formal verification.

**How often should I reassess?**
After any significant architectural change, after adding new agent capabilities or tool integrations, or quarterly for systems under active development.
