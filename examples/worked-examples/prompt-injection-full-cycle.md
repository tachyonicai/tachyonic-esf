# Worked Example: Prompt Injection Through All 10 Phases

This example traces prompt injection — the most prevalent AI attack class — through the full ESF maturation cycle.

## Phase 1: Name

Classify prompt injection subtypes within the taxonomy:

| ID | Subtype | Mechanism |
|---|---|---|
| PI-001 | Direct Instruction Override | "Ignore previous instructions and..." |
| PI-002 | Context Manipulation | Injecting false context to shift model behavior |
| PI-003 | Delimiter Exploitation | Breaking out of structured prompts via delimiters |
| PI-004-008 | Encoding Bypasses | Base64, ROT13, unicode smuggling, homoglyph substitution |
| PI-009-015 | Indirect Injection | Via retrieved documents, tool outputs, or external content |
| PI-016-020 | Advanced Techniques | Recursive injection, payload splitting, context overflow |

**Output:** 20 named, classified, severity-rated attack entries in `attack_catalog.yaml`.

## Phase 2: Relate

Map how prompt injection connects to other attack categories:

- PI → enables → SPL (injection extracts system prompt)
- PI → enables → EA (injection causes tool misuse)
- VE → enables → PI (RAG poisoning achieves indirect injection)
- VI → bypasses → PI defenses (image-embedded injection crosses modality)
- MT → enables → PI (multi-turn context builds toward injection)

**Key trust boundary:** The interface between untrusted user input and the model's instruction channel. This is where all PI attacks cross.

## Phase 3: Guess

Deploy detection and response heuristics:

- **Detection:** Pattern matching against known injection markers in user input. Encoding detection (base64, ROT13). Instruction-density scoring on retrieved documents.
- **Response:** Block inputs exceeding injection risk threshold. Suppress outputs containing system prompt fragments. Escalate session trust level after any detection event.
- **Circuit breakers:** If injection detection fires 3+ times in one session, isolate the session.

These are fast and imperfect. They catch naive attacks and miss sophisticated ones.

## Phase 4: Measure

Instrument every heuristic and test against reality:

- Run the 20 PI-series attack variants against the heuristic layer
- Measure: which variants are caught? Which bypass? At what false positive rate?
- Red team finding: encoding bypasses (PI-004-008) evade simple pattern matching. Multi-turn injection (MT-series feeding PI) evades per-message analysis.
- Labeled data: each test produces a TP/FP label that feeds Phase 5.

## Phase 5: Model

Build statistical baselines from operational data:

- **Baseline:** Normal user inputs have low instruction density. Score each input by instruction-to-data ratio.
- **Anomaly detection:** Inputs with instruction density above the 99th percentile of the baseline distribution are flagged, even if they don't match known injection patterns.
- **Information-theoretic monitoring:** Track entropy of user input sequences per session. Sudden entropy drops (from diverse queries to highly structured instruction-like content) signal potential injection.

This catches novel injection variants that no heuristic was designed for.

## Phase 6: Explain

Identify the root cause:

**Root cause:** The model processes instructions and data through the same channel. There is no structural distinction between "trusted system prompt" and "untrusted user input" at the token level.

**Architectural invariant:** If untrusted input were structurally separated from system instructions before processing, 20 PI attacks + 8 MT attacks + 8 VE attacks (36 of 122 total, 29%) would be eliminated by design.

**Counterfactual validation:** If instruction/data separation existed, PI-001 (Direct Instruction Override) becomes impossible — "ignore previous instructions" is tagged as data and never reaches the instruction channel.

## Phase 7: Formalize

Encode the invariant as deterministic policy:

```
RULE: input_instruction_separation
  FOR ALL inputs I:
    IF I.source = "user" OR I.source = "retrieval" OR I.source = "tool_output":
      I.channel = DATA
      I CANNOT be processed in INSTRUCTION channel
    
    IF I.source = "system_prompt" OR I.source = "pipeline_config":
      I.channel = INSTRUCTION

  ENFORCEMENT: deterministic, no override, no exceptions
```

Remediation as state transition: if a finding classified as PI-series reaches TP status, the finding lifecycle transitions through DETECTED → TRIAGED → EVIDENCED, with the human gate before DISCLOSED.

## Phase 8: Constrain

Make instruction/data conflation structurally impossible:

- **Architecture:** Separate instruction and data into distinct processing channels at the system level. User input, retrieved documents, and tool outputs are tagged as DATA before entering any processing pipeline. System prompts and pipeline configuration are tagged as INSTRUCTION.
- **Enforcement:** The tagging is architectural — there is no code path that processes DATA-tagged content as INSTRUCTION. This is not a runtime check; it is a structural property of the system.
- **Result:** PI-001 through PI-020 are eliminated not by detection but by the absence of a mechanism for user input to reach the instruction channel.

Note: Full instruction/data separation is an active research area in AI architecture. Current implementations approximate this through prompt engineering, but true structural separation at the model level is not yet achieved.

## Phase 9: Prove

Formally verify the separation property:

```
SPECIFICATION:
  For all execution traces T:
    For all tokens K in T:
      IF K.source ∈ {user, retrieval, tool_output}:
        K.channel = DATA at every processing step
      AND K never appears in INSTRUCTION channel at any step

PROPERTY TYPE: Safety ("nothing bad ever happens")

VERIFICATION: Model check all reachable states of the input processing 
  pipeline to confirm no state transition moves a DATA-tagged token 
  to the INSTRUCTION channel.
```

If the model checker finds a counterexample, it reveals a specific code path that violates the separation — an attack vector that no other phase discovered.

## Phase 10: Evolve

The cycle continues:

- New PI variants emerge (e.g., a novel encoding that bypasses the data channel tagging)
- The variant is detected by Phase 5 anomaly detection (it doesn't match known patterns but has anomalous instruction density)
- It's named as PI-021 in the taxonomy (Phase 1)
- Its relationship to existing attack chains is mapped (Phase 2)
- A heuristic is deployed to catch the specific encoding (Phase 3)
- The heuristic is measured (Phase 4)
- If the encoding bypass reveals a flaw in the structural separation, the Phase 8 architecture is updated and Phase 9 re-verification is triggered

Each cycle pushes the known PI boundary deeper into determinism while maintaining adaptive detection at the frontier.
