# Decision Guide: What Phase Should I Invest In Next?

Use this guide after completing a [maturity assessment](../rubric/assessment-scorecard.yaml) to determine where to focus next.

## Decision Tree

```
START
  │
  ├─ Do you have a structured taxonomy of threats? (Phase 1 ≥ 2?)
  │  NO → Invest in Phase 1. You can't secure what you can't name.
  │  YES ↓
  │
  ├─ Are trust boundaries and attack chains mapped? (Phase 2 ≥ 2?)
  │  NO → Invest in Phase 2. Isolated categories miss multi-stage attacks.
  │  YES ↓
  │
  ├─ Are detection and response heuristics deployed? (Phase 3 ≥ 2?)
  │  NO → Invest in Phase 3. Understanding without action is observation, not security.
  │  YES ↓
  │
  ├─ Are heuristics measured? (Phase 4 ≥ 2?)
  │  NO → Invest in Phase 4. Untested heuristics are superstitions.
  │  YES ↓
  │
  ├─ Is evolution happening? (Phase 10 ≥ 2?)
  │  NO → Invest in Phase 10. Without feedback loops, the system stagnates.
  │  YES ↓
  │
  ├─ Do you understand root causes? (Phase 6 ≥ 2?)
  │  NO → Invest in Phase 6. Detecting symptoms forever is expensive.
  │  YES ↓
  │
  ├─ Are root causes formalized as deterministic rules? (Phase 7 ≥ 2?)
  │  NO → Invest in Phase 7. Causal understanding without enforcement is research, not security.
  │  YES ↓
  │
  ├─ Are critical properties structurally enforced? (Phase 8 ≥ 2?)
  │  NO → Invest in Phase 8. Runtime checks can be bypassed; structural constraints cannot.
  │  YES ↓
  │
  └─ Are highest-consequence properties formally verified? (Phase 9 ≥ 2?)
     NO → Invest in Phase 9 for your most critical properties.
     YES → You're mature. Focus on expanding Phase 9 coverage and optimizing Phase 10.
```

## Priority Rules

When multiple phases need investment, prioritize by:

1. **Blocking dependencies first** — Phase 4 (Measure) is the most common blocker because every downstream improvement depends on data. If Phase 4 is weak, fix it before anything else.

2. **Consequence-weighted gaps** — A Phase 8 gap at a critical trust boundary is more urgent than a Phase 5 gap in interior monitoring.

3. **Quick wins** — Moving from Score 0 to Score 2 is usually cheaper than moving from Score 2 to Score 4. Take the easy wins to establish momentum.

4. **Phase 10 is never optional** — Even early-maturity systems need feedback loops. A system that doesn't evolve is a system that degrades.

## Common Mistakes

**Skipping Phase 6 (Explain) to jump to Phase 7 (Formalize):** You end up with deterministic rules that don't address root causes. When the threat landscape shifts, the rules become irrelevant.

**Investing in Phase 9 (Prove) before Phase 7-8 are solid:** Formal verification is expensive. Proving properties of a system that isn't yet structurally constrained is proving the wrong thing.

**Neglecting Phase 4 (Measure) because "we know it works":** Belief is not measurement. Every heuristic's performance degrades as threats evolve. Continuous measurement is the foundation of everything above it.

**Over-investing in Phase 5 (Model) when Phase 3 (Guess) has gaps:** Statistical models are powerful but slow. Fast heuristics as circuit breakers should cover every attack chain before you invest in statistical depth.
