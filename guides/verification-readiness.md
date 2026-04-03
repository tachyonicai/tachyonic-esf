# Decision Guide: Is This Property Ready for Formal Verification?

Formal verification (Phase 9) is the most expensive phase to execute. This guide helps you determine whether a property is ready — and worth the investment.

## Prerequisites Checklist

All five must be true before formal verification is justified.

| # | Prerequisite | Question | If NO |
|:-:|---|---|---|
| 1 | **Causal understanding (Phase 6)** | Do you understand *why* this property matters — what root cause it addresses? | Go back to Phase 6. Proving a property you don't causally understand risks proving the wrong thing. |
| 2 | **Formal specification (Phase 7)** | Can you express "correct behavior" as a precise, unambiguous formal statement? | Go back to Phase 7. Vague specifications produce meaningless proofs. |
| 3 | **Structural constraint (Phase 8)** | Is the system architecturally designed to support this property, or are you trying to prove an emergent behavior of an unconstrained system? | Go back to Phase 8. It's cheaper to constrain the architecture than to prove correctness of an unconstrained system. |
| 4 | **Highest consequence** | Is this among the highest-consequence properties in your system? Would a violation be catastrophic? | Consider stopping at Phase 8. Structural enforcement may be sufficient. |
| 5 | **Stable specification** | Is the property stable enough that the specification won't change before the proof is complete? | Wait. Proving a moving target wastes effort. |

## Property Classification

Different property types have different verification characteristics.

### Safety Properties ("Nothing bad ever happens")

- **Verification approach:** Show that no reachable state violates the property
- **Tractability:** Generally tractable — model checkers can explore reachable states
- **Examples:** "No untriaged finding reaches evidence packaging," "No agent exceeds its initialized privilege set"

### Liveness Properties ("Something good eventually happens")

- **Verification approach:** Show that progress is always possible and the system eventually reaches a desired state
- **Tractability:** Harder than safety — requires reasoning about infinite execution paths
- **Examples:** "The system always recovers to a safe state within bounded time," "Every flagged event is eventually reviewed"

### Bounded Properties ("Within limits")

- **Verification approach:** Show that quantitative bounds hold across all inputs
- **Tractability:** Often tractable via bounded model checking
- **Examples:** "Resource consumption never exceeds N," "Downstream spawn depth never exceeds K"

## Readiness Signals

**Strong signals the property IS ready:**
- The property has been expressed as formal state machine transitions (Phase 7)
- The architecture was designed to support the property (Phase 8)
- The property has been tested empirically with zero observed violations (Phase 4)
- The specification has been reviewed by domain experts and is unambiguous
- A violation would be catastrophic and unrecoverable

**Strong signals the property is NOT ready:**
- The specification contains "should" or "usually" instead of "always" or "never"
- The property depends on external systems whose behavior you don't control
- The threat the property addresses is still evolving (Phase 6 understanding is incomplete)
- The property hasn't been tested empirically (Phase 4 was skipped)
- The cost of verification exceeds the cost of the failure it prevents

## Verification Approach Selection

| System Size | Recommended Approach | Tools |
|---|---|---|
| Small state space (<10K states) | Exhaustive model checking | SPIN, NuSMV |
| Medium state space | Bounded model checking | TLA+, CBMC |
| Large/infinite state space | Theorem proving | Coq, Lean, Isabelle |
| Protocol-level properties | Protocol verification | TLA+, Promela/SPIN |
| Concurrent systems | Concurrency-aware model checking | SPIN, TLA+ |

## After Verification

- **Proof succeeded:** Document the specification, the proof, and the scope. Clearly state what IS and IS NOT covered. Maintain the proof alongside the codebase — a proof of a previous version guarantees nothing about the current version.
- **Proof failed (counterexample found):** The counterexample is valuable — it reveals an attack path that no other phase discovered. Feed it back to Phase 1 (taxonomy), Phase 2 (ontology), and Phase 3 (heuristics).
- **Verification is intractable:** Consider bounded model checking (verify up to depth N) or decompose the property into smaller, independently verifiable sub-properties.

## Re-verification Triggers

Formal verification must be re-run when:
- The system's state machine changes (new states, new transitions)
- The specification changes (new properties, modified definitions)
- Dependencies change (new tools, new agent capabilities)
- The trust boundary model changes (new interfaces, modified permissions)

Automate re-verification in CI where possible.
