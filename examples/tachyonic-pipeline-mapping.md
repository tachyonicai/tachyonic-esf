# Reference Implementation: Tachyonic Agentic Security Pipeline

This document maps the Tachyonic 11-stage security pipeline to the ESF, demonstrating how a real system implements the framework.

## System Overview

The Tachyonic pipeline is an agentic security research system that accepts a target (URL, repo, MCP server, voice endpoint) and a set of hypotheses, runs a full research methodology without human intervention, and self-improves with each campaign cycle.

```
INIT → RECON → SCAN → HEUR_TRIAGE → ANALYST_TRIAGE →
EVIDENCE → DOWNSTREAM_SPAWN → UPLOAD → NOTIFY → SELF_IMPROVE → DONE
```

## Pipeline ↔ ESF Mapping

| Pipeline Stage | ESF Phase(s) | Epistemological Role |
|---|---|---|
| **INIT** | Phase 1 (Name) | Target classification and hypothesis scoping — applying the taxonomy to a specific target |
| **RECON** | Phase 1→2 (Name → Relate) | Source review builds a target-specific ontology — entities, components, relationships, trust boundaries |
| **SCAN** | Phase 3 (Guess) | Broad pattern-matching heuristics across the 122-attack taxonomy |
| **HEUR_TRIAGE** | Phase 4 + 7 (Measure + Formalize) | 14 deterministic heuristics performing empirically validated FP suppression |
| **ANALYST_TRIAGE** | Phase 5→6 (Model → Explain) | Probabilistic classification (TP/FP/plausible) with causal reasoning |
| **EVIDENCE** | Phase 6→7 (Explain → Formalize) | Analyst understanding formalized into structured evidence packages |
| **DOWNSTREAM_SPAWN** | Phase 2 (Relate, applied) | Ontology traversal — findings imply related targets for investigation |
| **UPLOAD** | Phase 8 (Constrain) | Evidence integrity structurally enforced via checksums and immutable storage |
| **NOTIFY** | Operational | Delivery — Slack, email, webhook |
| **SELF_IMPROVE** | Phase 10 (Evolve) | Labeled data → heuristic generation → PR → evolution cycle |
| **DONE** | Phase 4 (Measure) | Campaign metrics recorded, closing the measurement cycle |

## Current Maturity Assessment

```
Phase:   1    2    3    4    5    6    7    8    9    10
         Name Rel  Gss  Msr  Mdl  Exp  Fml  Con  Prv  Evo
Score:   3-4  2    3    3    2-3  2    3    2    0-1  3
```

| Phase | Score | Rationale |
|---|---|---|
| 1. Name | 3-4 | 122-attack taxonomy, machine-readable YAML, extensible schema, multi-framework mapping |
| 2. Relate | 2 | OWASP/ATLAS mappings provide typed relationships; attack chain analysis exists; not yet a machine-readable graph with inference |
| 3. Guess | 3 | 14 operational heuristics, remediation guidance with code examples, documented and instrumented |
| 4. Measure | 3 | Per-heuristic metrics via analyst labels, self-improve feedback loop, adversarial hypothesis testing |
| 5. Model | 2-3 | Labeled data accumulating; statistical baselines emerging; explicit modeling infrastructure in progress |
| 6. Explain | 2 | Root cause analysis demonstrated (instruction/data conflation); cross-campaign causal analysis not yet systematic |
| 7. Formalize | 3 | 14-heuristic engine is deterministic, formal state transitions for finding lifecycle, coverage measurable |
| 8. Constrain | 2 | Evidence integrity, resource isolation, pipeline ordering structural; RECON hardening is a gap |
| 9. Prove | 0-1 | Properties informally reasoned about; no formal specification or verification yet |
| 10. Evolve | 3 | Self-improve produces labeled data, generates rules, opens PRs with human review gate |

## Priority Development Areas

1. **Phase 2 → Score 3**: Convert mappings into a machine-readable knowledge graph with inference
2. **Phase 6 → Score 3**: Systematize cross-campaign causal analysis
3. **Phase 8 → Score 3**: Structurally harden RECON and isolate agent capabilities per stage
4. **Phase 9 → Score 2**: Formally specify top-priority pipeline integrity properties

## Key Design Patterns

**The HEUR_TRIAGE → ANALYST_TRIAGE handoff** runs a formalized deterministic filter (Phase 7) followed by a causal reasoning agent (Phase 5-6). This is Phase 7 feeding into Phase 5-6, which is inverted from the theoretical sequence — and intentionally so. Cheap deterministic rules reduce the problem space before expensive causal reasoning is applied.

**The human gate on disclosure** (EVIDENCED → DISCLOSED) is a formal constraint — it cannot be bypassed by any automated path. This implements epistemological humility: the system can automate detection and evidence, but the decision to disclose requires human judgment.

**The SELF_IMPROVE → HEUR_TRIAGE loop** is the Phase 10 → Phase 7 promotion path working in production. Labeled data from campaigns generates candidate rules that, once reviewed and merged, become part of the deterministic triage engine.

## Related Resources

- Attack taxonomy: [tachyonic-heuristics](https://github.com/tachyonicai/tachyonic-heuristics)
- Blog post: [We Catalogued 122 Ways to Break AI Systems](https://tachyonicai.com/blog/122-attack-taxonomy/)
- Assessment service: [Tachyonic](https://tachyonicai.com)
