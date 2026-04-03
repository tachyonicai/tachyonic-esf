# Worked Example: Privilege Escalation Through All 10 Phases

This example traces privilege escalation in agentic AI systems — the risk that an agent gains capabilities beyond its intended scope — through the full ESF maturation cycle.

## Phase 1: Name

Classify privilege escalation subtypes:

| ID | Subtype | Mechanism |
|---|---|---|
| EA-001 | Parameter Injection | Manipulating tool call parameters to access unauthorized resources |
| EA-003 | Tool Chaining | Sequencing permitted tool calls to achieve an unpermitted outcome |
| EA-005 | Scope Escape | Agent acts outside its declared operational boundary |
| EA-007 | Capability Accumulation | Agent acquires new capabilities during execution not granted at initialization |
| EA-009 | Delegation Abuse | Agent delegates tasks to other agents, transferring or escalating privileges |
| EA-011 | SSRF via Agent | Agent-initiated requests reach internal services not intended to be accessible |

**Output:** 12 named EA-series attacks in the taxonomy, plus related ASI02 (Tool Misuse) and ASI03 (Privilege Compromise) from OWASP Agentic Top 10.

## Phase 2: Relate

Map the privilege escalation attack surface:

```
Agent → has → Capability Set (initialized at creation)
Capability → grants → Tool Access
Tool → operates-on → Asset
Asset → has → Sensitivity Level

Attack chain:
  JB (bypass guardrails) → EA-001 (inject tool parameters) → EA-003 (chain tools)
  → EA-007 (accumulate capabilities) → unauthorized asset access
```

**Key trust boundary:** The agent-tool interface. Every EA-series attack targets this single boundary. In multi-agent systems, the agent-agent delegation interface is a second critical boundary.

## Phase 3: Guess

Deploy heuristics at the agent-tool interface:

- **Scope guard:** If an agent requests a tool outside its declared capability set, deny by default
- **Parameter validation:** If tool call parameters reference resources outside the agent's scope, deny
- **Rate limiting:** If tool invocation rate exceeds 3x session baseline, pause and flag
- **Delegation constraint:** If an agent delegates to another agent with higher privileges, require explicit authorization
- **Budget ceiling:** Hard limit on total actions per session

## Phase 4: Measure

Test heuristics against the 12 EA-series attacks:

- Scope guards catch EA-005 (direct scope escape) but miss EA-003 (tool chaining within scope that achieves out-of-scope outcomes)
- Parameter validation catches EA-001 (obvious parameter injection) but misses subtle parameter manipulation
- Rate limiting produces high false positive rates for legitimate complex tasks
- Key finding: **EA-003 (tool chaining) bypasses per-action checks because each individual action is permitted — the escalation is emergent from the sequence**

This failure feeds back to Phase 1 (refine EA-003 definition) and Phase 6 (root cause analysis).

## Phase 5: Model

Build statistical models from operational data:

- **Baseline:** For each agent type, model the typical distribution of tool calls per session (which tools, in what order, at what frequency)
- **Sequence anomaly detection:** Flag tool call sequences that deviate from learned patterns, even if each individual call is within scope
- **Capability drift monitoring:** Track the effective privilege level of each action in a session. If the maximum privilege increases over the session, flag it.

This catches EA-003 (tool chaining) because the emergent privilege escalation shows up as a capability drift anomaly, even though each individual action passes the scope guard.

## Phase 6: Explain

Root cause analysis:

**Root cause:** Agent capabilities are checked per-action (policy enforcement), not per-sequence (structural enforcement). The permission model validates "can this agent call this tool?" but not "does this sequence of tool calls achieve an unpermitted outcome?"

**Architectural invariant:** Agent capabilities must be evaluated at the *outcome* level, not just the *action* level. A sequence of individually-permitted actions that achieves an unpermitted outcome must be treated as a privilege violation.

**Second root cause:** Capability scope is granted at initialization and not re-evaluated. An agent that legitimately receives expanded capabilities during a session (e.g., a user grants additional permissions) creates an attack surface — the agent's capability history becomes a vector for social engineering.

**Counterfactual:** If capabilities were structurally bounded (unforgeable tokens, per-action verification against intended outcomes), EA-003 through EA-009 would be eliminated.

## Phase 7: Formalize

Encode as deterministic policy:

```
RULE: capability_enforcement
  FOR ALL agents A and tool invocations T:
    T.permitted = TRUE IF AND ONLY IF:
      T.tool ∈ A.capability_set
      AND T.parameters ⊂ A.resource_scope
      AND T.outcome_privilege ≤ A.max_privilege
      AND A.session_privilege_history is monotonically non-increasing
        OR explicit_reauthorization has occurred

RULE: delegation_enforcement
  FOR ALL delegations D from agent A to agent B:
    B.capability_set ⊆ A.capability_set
    AND B.max_privilege ≤ A.max_privilege
    AND D requires explicit_authorization IF B.max_privilege > B.default_privilege
```

**Remediation state machine:**
```
NORMAL → FLAGGED (capability drift detected)
FLAGGED → PAUSED (human review required)
PAUSED → RESTORED (privileges confirmed legitimate) | TERMINATED (violation confirmed)
```

## Phase 8: Constrain

Make privilege escalation structurally impossible:

- **Capability-based security:** Agent capabilities are unforgeable tokens, not configuration strings. An agent cannot fabricate a capability it wasn't granted.
- **Outcome-level enforcement:** The tool proxy evaluates not just "is this action permitted?" but "does the cumulative outcome of this session's actions exceed the agent's privilege scope?" This is enforced at the proxy layer, not in the agent's own code.
- **Delegation as capability transfer:** When agent A delegates to agent B, capabilities are explicitly transferred (not copied or inherited). A's available capabilities decrease by the amount delegated. This prevents capability amplification through delegation chains.
- **Structural isolation:** Each agent runs in a separate execution context. There is no shared memory, no shared filesystem, no shared credential store between agents at different trust levels.

## Phase 9: Prove

Formally verify the privilege model:

```
SPECIFICATION:
  Safety property 1: "No agent ever holds a capability not granted at 
    initialization or through explicit reauthorization"
  
  Safety property 2: "No sequence of tool calls achieves an effective 
    privilege level exceeding the agent's max_privilege"
  
  Safety property 3: "Delegation never increases the total capability 
    in the system — capabilities are transferred, not duplicated"
  
  Liveness property: "An agent whose privileges are revoked terminates 
    or returns to safe state within bounded time"

VERIFICATION APPROACH: Model the agent-tool-capability system as a state 
  machine. Define capability sets, tool invocations, and delegations as 
  state transitions. Model check all reachable states for property violations.
```

A counterexample would reveal a specific sequence of actions that achieves privilege escalation despite the structural constraints — an extremely valuable finding.

## Phase 10: Evolve

The cycle continues:

- A new multi-agent orchestration pattern is deployed (e.g., agents that dynamically form working groups)
- The delegation model doesn't account for group-level capability aggregation — collectively, the group has capabilities no individual agent has
- This is detected by Phase 5 (capability drift anomaly at the group level)
- Named as EA-013 in the taxonomy
- The delegation enforcement rule in Phase 7 is updated to include group-level capability tracking
- Phase 8 structural constraints are extended to enforce group-level privilege bounds
- Phase 9 is re-run with the updated state machine

Each cycle discovers new escalation vectors created by new agent architectures, and pushes them through the hardening pipeline.
