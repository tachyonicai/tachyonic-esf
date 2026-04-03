# Decision Guide: Should I Formalize This or Keep It Heuristic?

Not every security property should be pushed to Phase 7+ (formal rules, structural constraints, verification). This guide helps you decide when formalization is worth the cost and when heuristics are the appropriate level.

## The Decision Matrix

Score each property on four dimensions, then use the matrix to decide.

### Dimension 1: Consequence of Failure

| Score | Level | Description |
|:-----:|-------|-------------|
| 1 | Low | Failure is annoying but tolerable (false alerts, minor delays) |
| 2 | Medium | Failure causes operational disruption (service degradation, data quality issues) |
| 3 | High | Failure causes significant harm (data breach, unauthorized actions, financial loss) |
| 4 | Critical | Failure is catastrophic (complete system compromise, safety-critical failure) |

### Dimension 2: Understanding Stability

| Score | Level | Description |
|:-----:|-------|-------------|
| 1 | Volatile | The threat changes weekly; new variants emerge constantly |
| 2 | Evolving | The threat changes monthly; patterns are somewhat predictable |
| 3 | Stable | The threat is well-understood; new variants are incremental |
| 4 | Settled | The threat mechanism is fully understood and unlikely to change |

### Dimension 3: Check Frequency

| Score | Level | Description |
|:-----:|-------|-------------|
| 1 | Rare | The check runs occasionally (weekly audits, periodic reviews) |
| 2 | Regular | The check runs daily or per-session |
| 3 | Frequent | The check runs per-request or per-action |
| 4 | Continuous | The check runs on every state transition in real time |

### Dimension 4: Trust Boundary Position

| Score | Level | Description |
|:-----:|-------|-------------|
| 1 | Interior | The property is inside a single trust domain; other defenses exist |
| 2 | Near-boundary | Close to a trust boundary but with defense-in-depth backup |
| 3 | At boundary | Sits directly at a trust boundary between components |
| 4 | Sole boundary | This IS the trust boundary; no other defense exists |

## Decision Rules

**Total score: sum of all four dimensions (4-16)**

| Total | Recommendation | Rationale |
|:-----:|----------------|-----------|
| 4-6 | **Keep as heuristic (Phase 3)** | Low consequence, volatile understanding, rare checks, interior position. Formalization cost exceeds benefit. |
| 7-9 | **Measure and model (Phase 4-5)** | Worth investing in empirical validation and statistical modeling, but formalization is premature. |
| 10-12 | **Formalize (Phase 7)** | High enough consequence and stability to justify deterministic rules. |
| 13-14 | **Constrain structurally (Phase 8)** | Critical enough and stable enough to justify architectural enforcement. |
| 15-16 | **Prove (Phase 9)** | Highest consequence, at sole trust boundary, continuous check, settled understanding. Mathematical proof is justified. |

## Worked Examples

**Example 1: Novel jailbreak detection**
- Consequence: 2 (medium — jailbreaks are serious but defense-in-depth exists)
- Stability: 1 (volatile — new jailbreak variants emerge weekly)
- Frequency: 3 (every user input)
- Position: 2 (near-boundary — other defenses exist downstream)
- **Total: 8 → Measure and model.** Keep heuristic detection, invest in statistical modeling to catch novel variants. Don't formalize — the rules would be outdated immediately.

**Example 2: Agent privilege escalation prevention**
- Consequence: 4 (critical — unauthorized actions on external systems)
- Stability: 4 (settled — the permission model is well-defined)
- Frequency: 4 (every tool invocation)
- Position: 4 (sole boundary — this is where agent meets tool)
- **Total: 16 → Prove.** This is the highest-priority candidate for formal verification.

**Example 3: System prompt leakage detection**
- Consequence: 2 (medium — leaked prompt reveals architecture but isn't catastrophic)
- Stability: 3 (stable — extraction techniques are well-catalogued)
- Frequency: 3 (every model output)
- Position: 2 (near-boundary — output filtering provides backup)
- **Total: 10 → Formalize.** Worth encoding as a deterministic output filter.

**Example 4: Token budget enforcement**
- Consequence: 2 (medium — resource exhaustion, cost overrun)
- Stability: 4 (settled — token counting is deterministic)
- Frequency: 4 (continuous)
- Position: 3 (at boundary — sits between agent and compute resources)
- **Total: 13 → Constrain structurally.** Enforce at the orchestration layer, not as a runtime check.

## Red Flags: When NOT to Formalize

- **You're formalizing from intuition, not from Phase 6 causal analysis.** Rules without causal grounding become brittle.
- **The heuristic's false positive rate isn't measured yet.** Formalizing a bad heuristic makes it a bad rule — harder to change.
- **The property crosses multiple abstraction levels.** If enforcement requires coordination across hardware, OS, and application layers, structural constraint (Phase 8) may be more appropriate than formal rules (Phase 7).
- **You're formalizing to avoid the discomfort of uncertainty.** Some properties genuinely belong at Phase 3-5 because the threat landscape is too volatile for determinism.
