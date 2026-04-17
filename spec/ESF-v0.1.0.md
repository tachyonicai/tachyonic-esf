# Evolutionary Security Framework (ESF)

### A Living Specification for Progressive Determinism in Agentic Security Systems

**Version:** 0.1.0-draft
**Status:** Living Document
**Created:** 2026-04-03
**Last Updated:** 2026-04-03

---

## Document Conventions

- **[STABLE]** — Section is well-defined and unlikely to change structurally
- **[DRAFT]** — Section is substantive but may evolve
- **[PLACEHOLDER]** — Section is reserved for future expansion
- **[EXAMPLE NEEDED]** — Concrete worked examples to be added

---

## 1. Executive Summary [STABLE]

The Evolutionary Security Framework (ESF) defines a ten-phase maturation model for agentic security systems. It describes the sequential progression from unstructured observation to mathematically proven correctness — the path from naming a problem to provably solving it.

The core thesis: **security matures by progressively converting uncertainty into structure.** Each phase takes something fuzzy and makes it more precise, more enforceable, more provable — while maintaining adaptive capacity at the frontier where new threats emerge.

The framework is:

- **Language-agnostic** — it describes epistemological phases, not implementation technologies
- **Domain-portable** — while designed for agentic AI security, the phases apply to any domain requiring progressive hardening
- **Assessment-ready** — any system can be scored against the framework to identify maturity levels and gaps
- **Cyclical** — it is not a one-time waterfall; the final phase feeds back into the first, creating a continuous hardening loop

### The Sequence in One Sentence

> Name → Relate → Guess → Measure → Model → Explain → Formalize → Constrain → Prove → Evolve

---

## 2. Foundational Principles [STABLE]

These principles underpin the entire framework and apply at every phase.

### 2.1 Progressive Determinism

The framework moves from low determinism (heuristics, intuition) to high determinism (formal proof). This is not a value judgment — every level of determinism has a role. The goal is to push each security property to the *appropriate* level of determinism given its consequence and maturity.

### 2.2 The Funnel Principle

Not everything moves to the highest phase. The distribution is intentionally pyramidal:

```
Phase 1-3:   ████████████████████████████  Many items
Phase 4-5:   ██████████████████            Fewer — measured and modeled
Phase 6-7:   ██████████                    Fewer still — explained and formalized
Phase 8-9:   ████                          Only the most critical — constrained and proven
Phase 10:    ████████████████████████████  Everything — evolution is universal
```

### 2.3 Appropriate Hardening

Push a security property toward higher determinism when:

- **High consequence** — failure is catastrophic
- **Stable understanding** — the threat is well-understood enough to formalize
- **High frequency** — the check runs constantly; false positives are costly at scale
- **Boundary enforcement** — it sits at a trust boundary between components

Keep it at lower determinism when:

- **Novel/evolving threats** — the landscape shifts too fast to formalize
- **Exploratory detection** — you're catching unknown-unknowns
- **Low consequence** — errors are tolerable
- **Interior monitoring** — defense-in-depth provides backup

### 2.4 Cyclical Maturation

The framework is not linear. It is a spiral. Every cycle through Phase 10 (Evolve) restarts the sequence at Phase 1 — but at a higher baseline. Known threats get pushed deeper into determinism with each cycle. New threats enter at Phase 1.

### 2.5 Self-Application

The framework applies to itself. A system built on this framework must be assessed *by* this framework — including the system's own attack surface, its own knowledge construction, and its own evolution mechanisms.

### 2.6 Epistemological Humility

No system achieves Phase 9 for all properties. The frontier of unknown threats never disappears. The framework explicitly preserves space for uncertainty (Phases 1-3) alongside certainty (Phases 7-9). A system that claims full determinism has a blind spot, not a solution.

---

## 3. The Ten Phases [STABLE]

### Overview Table

| Phase | Verb | Question | Technical Domain | Moves From → To |
|-------|------|----------|-----------------|-----------------|
| 1 | **Name** | What exists? | Taxonomy | Chaos → Categories |
| 2 | **Relate** | How does it connect? | Ontology | Categories → Structure |
| 3 | **Guess** | What might go wrong? | Heuristics | Structure → Intuition |
| 4 | **Measure** | Does it actually work? | Empirical Validation | Intuition → Evidence |
| 5 | **Model** | What patterns emerge? | Statistical / Information-Theoretic Modeling | Evidence → Prediction |
| 6 | **Explain** | Why does it happen? | Causal Inference | Prediction → Understanding |
| 7 | **Formalize** | What's always true? | Formal Logic / Policy Systems | Understanding → Rules |
| 8 | **Constrain** | What's impossible? | Structural Enforcement | Rules → Architecture |
| 9 | **Prove** | Can we guarantee it? | Formal Verification | Architecture → Certainty |
| 10 | **Evolve** | What's next? | Meta-heuristics / Adaptive Systems | Certainty → New Questions |

---

### Phase 1: Name (Taxonomy) [STABLE]

**Core Question:** *What exists in this domain?*

**Definition:** Identify and classify every entity, threat, asset, and action in the system. Assign precise names and positions within a structured hierarchy. Taxonomy is the act of imposing categorical order on an undifferentiated problem space.

**Inputs:**
- A domain or target to be secured
- Raw observations, threat intelligence, prior knowledge

**Outputs:**
- A structured catalog of entity types, threat types, asset types, and action types
- A hierarchical classification scheme with defined granularity levels
- A shared vocabulary that all subsequent phases depend on

**Core Concepts:**

| Term | Definition |
|------|-----------|
| **Taxonomy** | A hierarchical classification system that groups entities into categories and subcategories based on shared properties |
| **Faceted classification** | Organizing entities along multiple independent dimensions simultaneously (e.g., a threat classified by vector AND severity AND target AND actor) |
| **Meronymy** | Part-of relationships — describing what components compose an entity |
| **Polyhierarchy** | An entity belonging to multiple categories simultaneously; a single thing that is many kinds of thing |
| **DIKW pyramid (data level)** | The base of the Data → Information → Knowledge → Wisdom hierarchy; raw observations before they carry meaning |

**Principles:**
- You cannot reason about what you cannot name
- Classification precedes all other analysis — ambiguous vocabulary propagates errors through every subsequent phase
- Taxonomies should be exhaustive within their scope (every entity has a place) and mutually exclusive at each level (no entity occupies two sibling categories without explicit polyhierarchy)
- Granularity should match operational need — too coarse loses signal, too fine creates noise

**Anti-Patterns:**
- **Naming by analogy only** — calling something "like a firewall" instead of defining precisely what it is
- **Implicit taxonomy** — categories that exist in team members' heads but are never formalized
- **Frozen taxonomy** — a classification scheme that doesn't evolve as new entity types emerge
- **Taxonomy without scope** — trying to classify everything in the universe instead of bounding the domain

**Decision Criteria:**
- Is every entity in the system classifiable under the taxonomy?
- Can two people independently classify the same entity and arrive at the same category?
- Does the taxonomy distinguish entities that require different security treatment?

**Worked Example: The Tachyonic Attack Taxonomy**

The [tachyonic-heuristics](https://github.com/tachyonicai/tachyonic-heuristics) taxonomy is a reference implementation of Phase 1. It systematically catalogues over 140 distinct AI/LLM attack techniques across 13 categories, each mapped to industry frameworks (OWASP LLM Top 10, MITRE ATLAS).

*Taxonomy structure:*

| Category | ID Prefix | Count | Framework |
|---|---|---|---|
| Prompt Injection | PI | 20 | LLM01 |
| System Prompt Leakage | SPL | 12 | LLM07 |
| Jailbreaks | JB | 22 | LLM01 |
| Vision/Multimodal | VI | 12 | LLM01 |
| Excessive Agency / Tool Abuse | EA | 16 | LLM06 |
| Multi-Turn Manipulation | MT | 8 | LLM01 |
| Sensitive Information Disclosure | SID | 10 | LLM02 |
| Supply Chain | SC | 12 | LLM03 |
| Vector/Embedding Attacks | VE | 10 | LLM08 |
| Improper Output Handling | IOH | 8 | LLM05 |
| Unbounded Consumption | UC | 2 | LLM10 |
| Misinformation | MIS | 6 | LLM09 |
| Memory/Context Poisoning | CTX | 6 | ASI06 |
| **Total** | | **144** | |

*Each attack entry includes:*

- **ID** — Unique identifier (e.g., PI-001, JB-015, MT-003) providing stable reference across the system
- **Name** — Human-readable attack name
- **Category** — Which of the 13 categories it belongs to
- **Description** — What the attack does and how it works conceptually
- **Severity** — Critical, high, medium, or low
- **OWASP Mapping** — Which OWASP LLM Top 10 item it maps to
- **MITRE ATLAS Mapping** — Corresponding MITRE technique (where applicable)

*Why this is strong Phase 1 work:*

- **Exhaustive within scope** — 144 attacks cover the full documented AI attack surface, not just the well-known handful
- **Faceted classification** — attacks are classified by category, severity, and framework mapping (three independent dimensions)
- **Stable identifiers** — the ID scheme (PI-001, JB-015) provides unambiguous reference across teams, tools, and documentation
- **Extensible schema** — YAML schema in `schema/attack_schema.yaml` allows community contribution of new attack definitions following the same format
- **Machine-readable** — YAML format enables automated consumption by downstream phases (scanning, triage, detection)

*Phase 1 maturity assessment for tachyonic-heuristics:* **Score 3-4** — The taxonomy is machine-readable, consistently structured, mapped to multiple industry frameworks, and extensible. It reaches Score 4 when dynamic update mechanisms (automated gap detection from Phase 10 feedback) are operational.

*Key insight from the taxonomy:* Most AI security discussions focus on a handful of well-known attacks. In reality, the attack surface spans 13 distinct categories with over 140 techniques. A system that blocks a naive instruction override (PI-001) might still fall to an encoding bypass (PI-series), a multi-turn escalation (MT-series), or an indirect injection through retrieved content (VE-series). The taxonomy makes this breadth visible and actionable.

*Repository:* [github.com/tachyonicai/tachyonic-heuristics](https://github.com/tachyonicai/tachyonic-heuristics) (Apache 2.0)

---

### Phase 2: Relate (Ontology) [STABLE]

**Core Question:** *How do named things connect to each other?*

**Definition:** Define formal relationships between taxonomic categories. Ontology transforms a flat catalog into a connected graph of entities, properties, relationships, and constraints. It specifies not just what things exist, but how they interact, depend on, enable, and constrain each other.

**Inputs:**
- The taxonomy from Phase 1
- Domain expertise about how entities interact
- Known attack patterns and dependency chains

**Outputs:**
- A knowledge graph of entities and their typed relationships
- A schema defining permitted entity types, relationship types, and constraints
- Trust boundary maps showing where trust assumptions change
- Attack chain models showing how threats traverse relationships

**Core Concepts:**

| Term | Definition |
|------|-----------|
| **Ontology** | A formal model of entities, their properties, and the relationships between them — the "grammar" that defines how taxonomic "vocabulary" combines |
| **Knowledge graph** | A concrete instantiation of an ontology as a network of nodes (entities) and edges (relationships) |
| **Schema** | The blueprint defining what types of nodes and edges are allowed in the knowledge graph |
| **Semantic web / RDF / OWL** | Standards for making ontological knowledge machine-readable and interoperable across systems |
| **Inference** | Deriving new knowledge from existing relationships (if A→B and B→C, then A→C) |
| **Transitivity** | A property of relationships where A→B and B→C implies A→C |
| **Symmetry** | A property of relationships where A→B implies B→A |
| **Reflexivity** | A property of relationships where A→A is always true |
| **Open-world assumption** | The principle that absence of a fact does not mean it is false — critical for security where unknown relationships may exist |
| **Reification** | Making statements about statements (e.g., "this threat classification was assigned by X with Y confidence") |
| **Trust boundary** | An interface where trust assumptions change between components |

**Principles:**
- Isolated categories are inert; relationships create meaning — and vulnerability
- Attack chains are paths through the ontology; if you can't model the path, you can't detect the traversal
- The open-world assumption is the default for security — assume unknown relationships exist until proven otherwise
- Trust boundaries are the highest-value relationships to map; every boundary crossing is a potential vulnerability

**Anti-Patterns:**
- **Flat ontology** — defining entities and relationships with no depth or hierarchy
- **Missing trust boundaries** — modeling components without explicitly marking where trust assumptions change
- **Static ontology** — treating the relationship model as fixed when the system it describes is evolving
- **Ontology without inference** — building a knowledge graph but never deriving new relationships from existing ones
- **Completeness assumption** — believing the ontology captures all relationships that exist in reality

**Decision Criteria:**
- Does the ontology capture every trust boundary in the system?
- Can known attack chains be represented as paths through the ontology?
- Are relationship types explicitly typed with properties (transitivity, symmetry, etc.)?
- Is the ontology machine-readable, or does it exist only in human documentation?

**Worked Example: Ontological Relationships in the Attack Taxonomy**

The [tachyonic-heuristics](https://github.com/tachyonicai/tachyonic-heuristics) taxonomy provides the naming (Phase 1). The ontological layer emerges from the relationships *between* those named entities — relationships that the repository's mapping files begin to capture.

*Framework mappings as ontological relationships:*

The repository contains `taxonomy/owasp_mapping.yaml` and `taxonomy/atlas_mapping.yaml`. These are not just cross-references — they encode ontological relationships:

- **Attack → exploits → Vulnerability Class** (OWASP mapping): PI-001 through PI-020 all exploit LLM01 (Prompt Injection), but so do MT-001 through MT-008 (Multi-Turn Manipulation). The ontology reveals that multi-turn manipulation is a *variant mechanism* for the same underlying vulnerability class.
- **Attack → maps-to → Adversarial Technique** (ATLAS mapping): MITRE ATLAS provides a complementary relationship graph showing how AI-specific attacks relate to broader adversarial tradecraft.

*Cross-category attack chains visible in the ontology:*

The blog post accompanying the taxonomy identifies critical cross-category relationships that a flat taxonomy alone doesn't capture:

- **Prompt Injection (PI) → enables → System Prompt Leakage (SPL)**: A successful prompt injection can be used to extract the system prompt, which reveals architecture and constraints.
- **System Prompt Leakage (SPL) → informs → Jailbreak (JB)**: A leaked system prompt provides the blueprint for crafting targeted jailbreaks that exploit known constraints.
- **Jailbreak (JB) → enables → Excessive Agency (EA)**: Once safety guardrails are bypassed, tool abuse and privilege escalation become possible.
- **Vision/Multimodal (VI) → bypasses → Prompt Injection defenses (PI)**: Text-based input filters don't catch malicious instructions embedded in images — the attack crosses modality boundaries.
- **Vector/Embedding Attacks (VE) → enables → Prompt Injection (PI)**: Poisoned documents in a RAG system achieve indirect prompt injection through the retrieval pipeline.

These chains are paths through the ontology. Each path represents a multi-stage attack scenario that no single category fully describes.

*Trust boundary model derived from the taxonomy:*

The Excessive Agency (EA) category implicitly defines the critical trust boundary in agentic systems: the interface between the AI agent and its tool capabilities. The 12 attacks in this category (parameter injection, tool chaining, scope escape, SSRF through agent requests) all target this single boundary. The ontology makes explicit what the taxonomy implies: **the agent-tool interface is the highest-risk trust boundary in agentic AI systems.**

*Ontological relationships the taxonomy does not yet capture (growth areas):*

- **Attack → requires → Precondition**: Which attacks require other attacks to succeed first (dependency chains)?
- **Attack → targets → Architectural Component**: Which specific components (planner, executor, retrieval layer, tool proxy) does each attack target?
- **Defense → mitigates → Attack**: Formal mapping from remediation strategies back to specific attack IDs
- **Attack → produces → Observable Signal**: What evidence does each attack leave? This feeds Phase 3 (heuristic detection)

*Phase 2 maturity assessment for tachyonic-heuristics:* **Score 2** — Framework mappings (OWASP, ATLAS) provide typed relationships, and attack chain analysis in the blog post identifies cross-category paths. Score 3 requires the ontology to be machine-readable as a graph (not just YAML cross-references) with inference capability. Score 4 requires dynamic ontology updates from operational data.

---

### Phase 3: Guess (Heuristics) [STABLE]

**Core Question:** *What rules of thumb catch problems fast?*

**Definition:** Generate rapid, imperfect detection and response rules based on the ontological model. Heuristics are educated guesses — patterns that are likely to indicate threats, paired with response actions that are likely to mitigate them. They are deployed before validation because imperfect action beats perfect analysis.

**Inputs:**
- The ontology from Phase 2 (especially attack chain paths)
- Domain expertise and intuition
- Known threat patterns from external intelligence

**Outputs:**
- Detection heuristics — "if this pattern appears, flag it"
- Response heuristics — "if flagged, take this action" (block, pause, escalate, isolate, rollback)
- Initial thresholds and configuration parameters
- A working but unvalidated security layer

**Core Concepts:**

| Term | Definition |
|------|-----------|
| **Heuristic** | A practical rule of thumb that produces approximately correct results without formal guarantees |
| **Circuit breaker** | A heuristic that halts processing when predefined thresholds are exceeded, preventing cascade failures |
| **Scope guard** | A heuristic that restricts an agent's actions to a predefined operational boundary |
| **Budget constraint** | A heuristic that limits resource consumption (tokens, API calls, compute time, cost) |
| **Defense in depth** | Layering multiple independent heuristics so that an attack evading one encounters another |
| **Pattern matching** | Comparing observed behavior against known threat signatures |

**Principles:**
- Imperfect action beats perfect analysis — deploy heuristics before they're validated
- Pair every detection heuristic with a response heuristic — detection without response is observation, not security
- Heuristic diversity beats heuristic precision — multiple weak detectors layered together outperform a single strong one
- Default to restrictive — when uncertain, the heuristic should deny rather than permit
- Heuristics are expendable — they exist to be replaced by better mechanisms as understanding matures

**Anti-Patterns:**
- **Heuristic worship** — treating rules of thumb as if they were formal guarantees
- **Single-layer heuristics** — relying on one detection rule for a critical threat
- **Detection without response** — flagging threats but having no automated mitigation
- **Threshold paralysis** — spending excessive time tuning thresholds before deploying
- **Heuristic sprawl** — accumulating rules without organization, creating an unmanageable ruleset

**Decision Criteria:**
- Does every attack chain in the ontology have at least one detection heuristic covering it?
- Does every detection heuristic have a paired response action?
- Are heuristics independent enough that compromising one doesn't compromise others?
- Is the heuristic layer deployable and operational, even if imperfect?

**Worked Example: Deriving Heuristics from the Attack Taxonomy**

The [tachyonic-heuristics](https://github.com/tachyonicai/tachyonic-heuristics) repository contains `remediation/by_owasp.yaml` with defensive guidance per OWASP category, and `remediation/code_examples/` with input validation and output sanitization patterns. These are Phase 3 artifacts — heuristic detection and response rules derived from the taxonomic and ontological understanding of Phases 1-2.

*Deriving detection heuristics from attack chains:*

For each attack chain identified in Phase 2, the question is: "What observable signal would indicate this chain is being traversed?"

| Attack Chain | Detection Heuristic | Response Heuristic |
|---|---|---|
| PI → SPL (injection extracts system prompt) | Detect output containing fragments of known system prompt content | Suppress output, log event, flag session |
| SPL → JB (leaked prompt informs jailbreak) | Detect subsequent inputs referencing internal system prompt structure or constraint names | Escalate trust level of session, apply stricter filtering |
| JB → EA (jailbreak enables tool abuse) | Detect tool invocations following a session flagged for jailbreak indicators | Block tool access for flagged sessions, require re-authentication |
| VI → PI (image-embedded injection) | Detect text extracted from images containing instruction-like patterns | Apply same input validation to OCR-extracted text as to direct text input |
| VE → PI (RAG poisoning enables injection) | Detect retrieved documents with anomalous instruction density | Score retrieved documents for injection risk before including in context |

*Heuristics from the remediation layer:*

The `remediation/code_examples/input_validation.py` and `output_sanitization.py` files implement concrete heuristic patterns:

- **Input validation heuristics**: Pattern matching against known injection markers, encoding detection (base64, ROT13, unicode smuggling), instruction-like content scoring, delimiter exploitation detection
- **Output sanitization heuristics**: System prompt fragment detection in outputs, PII leakage scanning, code injection pattern detection in generated content, hallucination markers in structured outputs

*The 14-heuristic triage engine (pipeline context):*

In the agentic security pipeline, the HEUR_TRIAGE stage runs a Rust engine with 14 formalized heuristics that suppress false positives. These 14 heuristics represent Phase 3 rules that have been empirically validated (Phase 4) and promoted to formalized status (Phase 7) — they are deterministic, not probabilistic. They operate as a fast, cheap filter before the more expensive ANALYST_TRIAGE (Claude agent, Phase 5-6).

This demonstrates the funnel principle in action: 144 attack types in the taxonomy → scanned broadly by the scanner → filtered deterministically by 14 hardened heuristics → analyzed causally by the AI analyst for the remainder.

*Phase 3 maturity assessment for tachyonic-heuristics:* **Score 3** — Heuristics are documented, paired with response actions, deployed operationally, and the 14-heuristic engine is instrumented with FP suppression metrics. Score 4 requires automated heuristic generation from new taxonomy entries and continuous threshold optimization from Phase 10 feedback.

---

### Phase 4: Measure (Empirical Validation) [STABLE]

**Core Question:** *Do our guesses actually work?*

**Definition:** Instrument every heuristic and systematically measure its performance against reality. Testing converts belief into knowledge. This phase produces the empirical data that all subsequent phases depend on.

**Inputs:**
- Deployed heuristics from Phase 3
- Real-world operational data (agent sessions, actions, outcomes)
- Adversarial testing results (red team campaigns)

**Outputs:**
- Per-heuristic performance metrics (true positive rate, false positive rate, detection latency, bypass rate)
- A scored heuristic inventory with known strengths and weaknesses
- Identified blind spots and coverage gaps
- Failure classifications that feed back to Phase 1 (new threat categories)
- Labeled datasets for Phase 5 (model training)

**Core Concepts:**

| Term | Definition |
|------|-----------|
| **Signal-to-noise ratio** | The proportion of meaningful detections versus irrelevant alerts; a measure of heuristic precision |
| **False positive rate** | The frequency at which benign activity is incorrectly flagged as a threat |
| **False negative rate** | The frequency at which actual threats are missed by detection |
| **Red teaming** | Adversarial testing where a dedicated team attempts to bypass security controls |
| **Feedback loop** | A mechanism where measurement outcomes inform adjustments to the system being measured |
| **Labeled data** | Observations tagged with ground truth (true positive, false positive, etc.) that enable supervised learning |
| **Redundancy** | Deliberate duplication of detection mechanisms that enables cross-validation and resilience |

**Principles:**
- Untested heuristics are superstitions — measurement converts belief into knowledge
- Measure heuristics individually AND in combination — interactions between rules may produce emergent behavior
- Red teaming is not optional — adversarial testing reveals failure modes that operational data misses
- Every failure is a data point — classify failures by type and feed them back to Phase 1 as potential new taxonomy entries
- Measurement must be continuous, not one-time — heuristic performance degrades as threats evolve

**Anti-Patterns:**
- **Launch and forget** — deploying heuristics without ongoing measurement
- **Aggregate-only metrics** — measuring system-level performance without per-heuristic breakdown
- **Friendly-only testing** — measuring against known threats without adversarial probing
- **Metric fixation** — optimizing for measurable proxies (false positive rate) at the expense of unmeasured properties (novel threat detection)
- **Delayed measurement** — accumulating heuristics before establishing measurement infrastructure

**Decision Criteria:**
- Is every heuristic individually instrumented with performance metrics?
- Is the system regularly subjected to adversarial testing?
- Do failures produce structured data that feeds back to taxonomy and ontology?
- Is labeled data being generated that can train statistical models in Phase 5?

**Worked Example: Measuring Triage Heuristics in the Tachyonic Pipeline**

The agentic security pipeline's HEUR_TRIAGE → ANALYST_TRIAGE → SELF_IMPROVE chain is a concrete implementation of Phase 4 measurement.

*Measurement points in the pipeline:*

- **HEUR_TRIAGE output**: Each of the 14 heuristics produces a binary decision (keep/suppress) for every scan finding. The Rust engine logs which heuristic fired, what it suppressed, and what it passed through.
- **ANALYST_TRIAGE labels**: The Claude agent classifies each surviving finding as TP (true positive), FP (false positive), or plausible. These labels serve as ground truth for measuring the heuristic layer's performance.
- **SELF_IMPROVE evaluation**: At the end of each campaign, the labeled data is used to compute per-heuristic metrics — what did each heuristic correctly suppress? What did it incorrectly suppress? What FPs did it miss?

*Per-heuristic metrics derived:*

| Metric | What It Measures | Source |
|---|---|---|
| True suppression rate | Fraction of FPs correctly suppressed by the heuristic | ANALYST_TRIAGE labels vs. HEUR_TRIAGE decisions |
| False suppression rate | Fraction of TPs incorrectly suppressed | ANALYST_TRIAGE labels for findings that never reached analyst |
| Pass-through FP rate | FPs that survived heuristic filtering and reached the analyst | ANALYST_TRIAGE FP labels on passed findings |
| Heuristic coverage | Which taxonomy categories (of 144) does this heuristic apply to? | Mapping heuristic scope to taxonomy IDs |

*The feedback loop:*

When ANALYST_TRIAGE consistently labels a finding pattern as FP that HEUR_TRIAGE passed through, this signals a missing heuristic. SELF_IMPROVE generates a candidate rule, opens a PR, and — once reviewed and merged — the 14-heuristic count becomes 15. This is the Phase 4 → Phase 10 → Phase 3 cycle in practice.

Conversely, when ANALYST_TRIAGE labels something as TP that HEUR_TRIAGE suppressed (detected through sampling or audit), the offending heuristic's threshold is adjusted or the heuristic is flagged for review.

*Red teaming integration:*

The pipeline accepts hypothesis sets at INIT. These hypotheses can include adversarial scenarios designed to test specific heuristics — effectively an automated red team against the pipeline's own detection layer. Results feed back into Phase 4 metrics.

*Phase 4 maturity assessment:* **Score 3** — Per-heuristic metrics are tracked, labeled data feeds back to taxonomy and heuristic updates, and the SELF_IMPROVE stage closes the feedback loop. Score 4 requires continuous real-time metric tracking (not just per-campaign) and automated anomaly detection on the metrics themselves (detecting when a heuristic's performance degrades).

---

### Phase 5: Model (Statistical / Information-Theoretic Modeling) [STABLE]

**Core Question:** *What patterns emerge that human intuition missed?*

**Definition:** With sufficient empirical data, shift from human-authored rules to data-derived models. Build statistical baselines of normal behavior and let anomalies surface mathematically. This phase extends perception beyond human intuition into higher-dimensional pattern spaces.

**Inputs:**
- Labeled datasets from Phase 4
- Behavioral logs and action sequences
- Ontological structure from Phase 2 (for feature engineering and graph-based modeling)

**Outputs:**
- Behavioral baselines (statistical distributions of normal activity)
- Anomaly detection models (flag deviations from baseline)
- Classification models (given a flagged event, predict threat type from taxonomy)
- Information-theoretic monitoring thresholds (entropy, divergence measures)
- Discovered patterns that humans didn't anticipate

**Core Concepts:**

| Term | Definition |
|------|-----------|
| **Entropy** | A measure of uncertainty or surprise in a system; high entropy indicates unpredictability. In security: sudden entropy changes in agent behavior signal potential compromise |
| **KL divergence (Kullback-Leibler)** | Measures how one probability distribution differs from another; used to detect behavioral drift from an established baseline |
| **Mutual information** | Quantifies how much knowing one variable tells you about another; useful for feature selection in threat detection |
| **Cross-entropy** | Measures how well a model's predictions match observed reality; the foundation of most AI loss functions |
| **Anomaly detection** | Identifying observations that deviate significantly from learned patterns of normal behavior |
| **Embeddings** | Compressed vector representations of concepts that preserve semantic relationships — the bridge between symbolic knowledge and numerical computation |
| **Latent space** | The hidden structure a model discovers; an implicit ontology learned from data rather than defined by humans |
| **Channel capacity** | The maximum rate at which information can be reliably transmitted; relevant to bottlenecks in agent communication and monitoring |
| **Redundancy (information-theoretic)** | Deliberate or inherent duplication in information that enables error detection and correction |

**Principles:**
- Data sees dimensions that human intuition cannot — statistical models extend perception, not replace judgment
- Baselines must be established on verified-clean data; a baseline built on compromised behavior encodes the compromise
- Anomaly detection catches unknown-unknowns by definition — this is where novel threats first become visible
- Information-theoretic measures (entropy, divergence) are model-agnostic and can monitor any system with observable state transitions
- Statistical models supplement heuristics — they add depth, not replace the fast circuit-breakers of Phase 3

**Anti-Patterns:**
- **Model as oracle** — treating statistical outputs as ground truth rather than probabilistic indicators
- **Poisoned baselines** — training behavioral baselines on data that includes undetected attacks
- **Feature blindness** — building models that ignore the ontological structure and treat all inputs as flat feature vectors
- **Overfitting to history** — models that perfectly predict past attacks but fail on novel ones
- **Threshold rigidity** — setting anomaly thresholds once and never adapting them as behavior distributions evolve

**Decision Criteria:**
- Are behavioral baselines established on validated clean data?
- Can the models detect anomalies that no heuristic in Phase 3 was designed for?
- Are information-theoretic metrics (entropy, divergence) being monitored in real time?
- Do model outputs carry calibrated confidence scores, not just binary classifications?

**Worked Example: Behavioral Modeling Across Campaign Data**

As the Tachyonic pipeline runs campaigns against diverse targets (URLs, repos, MCP servers, voice endpoints), it accumulates labeled session data from ANALYST_TRIAGE. This data enables Phase 5 modeling.

*Behavioral baselines by target type:*

Different target types exhibit different vulnerability profiles. Statistical modeling across campaigns reveals:

- **MCP server targets** tend to cluster around Excessive Agency (EA) and Prompt Injection (PI) categories — tool-use interfaces expand the attack surface
- **Voice endpoint targets** show higher rates of Jailbreak (JB) success — audio modality adds encoding ambiguity that text-based defenses miss
- **Repository targets** cluster around Supply Chain (SC) and Improper Output Handling (IOH) — the attack surface is in dependencies and generated code
- **Web URL targets** spread across PI, SPL, and VI categories — standard web-facing AI attack surfaces

These profiles become statistical baselines. When a new MCP server target produces an unusual cluster of VE (Vector/Embedding) findings instead of the expected EA/PI distribution, the entropy of the finding distribution has shifted — signaling either a novel architecture or a novel attack surface.

*Information-theoretic monitoring:*

- **Entropy of finding distribution per campaign**: A campaign producing findings spread evenly across many categories (high entropy) suggests broad exposure. A campaign producing findings concentrated in one category (low entropy) suggests a specific architectural weakness.
- **KL divergence from target-type baseline**: Measures how much a specific campaign's finding distribution deviates from the expected distribution for that target type. High divergence triggers deeper investigation.
- **Mutual information between scan signals and analyst labels**: Which scanner outputs are most predictive of true positives? This drives feature selection for automated triage improvement.

*Phase 5 maturity assessment:* **Score 2-3** — Behavioral baselines become possible once sufficient campaign data accumulates. The pipeline's SELF_IMPROVE stage provides the labeled data. Score 3 requires explicit statistical baseline computation and divergence monitoring. Score 4 requires continuously retrained models with calibrated confidence scores on finding classification.

---

### Phase 6: Explain (Causal Inference) [STABLE]

**Core Question:** *Why do these vulnerabilities exist?*

**Definition:** Move from correlation to causation. Identify the structural properties of the system that *allow* vulnerabilities to exist, rather than merely detecting their symptoms. This phase produces architectural invariants — properties that, if guaranteed, would eliminate entire classes of threats.

**Inputs:**
- Statistical patterns from Phase 5
- Attack chain models from Phase 2
- Root cause data from failed heuristics (Phase 4)
- Cross-campaign analysis data (if available)

**Outputs:**
- Causal models linking architectural properties to vulnerability classes
- Identified architectural invariants (properties that eliminate threat classes if guaranteed)
- Counterfactual analysis ("if this property held, this attack class would be impossible")
- Prioritized invariant list ranked by attack surface reduction

**Core Concepts:**

| Term | Definition |
|------|-----------|
| **Causal inference** | Reasoning about cause-and-effect relationships, not just correlations; answering "why" rather than "what" |
| **Bayesian network** | A probabilistic graphical model that represents causal relationships with conditional probabilities |
| **Counterfactual reasoning** | Asking "what would have happened if X were different?" — essential for identifying root causes |
| **Root cause analysis** | Tracing a failure or vulnerability back to the fundamental property that enabled it |
| **Architectural invariant** | A property of the system that, if guaranteed, eliminates one or more classes of threats |
| **Kolmogorov complexity** | The length of the shortest program that can produce a given output; relates to the fundamental compressibility and simplicity of an explanation |
| **Minimum description length (MDL)** | The principle that the best model is the one that compresses data most efficiently; connects to Occam's razor — the simplest explanation that fits the evidence is preferred |
| **Compositionality** | The principle that complex meaning (or complex attacks) are built from simpler parts in structured ways |

**Principles:**
- Detecting symptoms indefinitely is expensive; understanding causes enables elimination
- A good causal model lets you reason about interventions — "if we change X, threats Y and Z become impossible"
- Not all causes are actionable — prioritize invariants that are both architecturally enforceable and high-impact
- Causal understanding is the bridge between detection (Phases 3-5) and prevention (Phases 7-9)
- The simplest causal explanation that accounts for the evidence is preferred (MDL / Occam's razor)

**Anti-Patterns:**
- **Correlation as causation** — assuming that co-occurring patterns have a causal relationship
- **Root cause singularity** — insisting every vulnerability has exactly one root cause when multiple factors may interact
- **Untestable causation** — proposing causal models that can't be validated by intervention or counterfactual analysis
- **Invariant inflation** — identifying too many "critical" invariants, diluting focus and making formalization intractable
- **Premature formalization** — jumping to Phase 7 before the causal model is sufficiently validated

**Decision Criteria:**
- Can the causal model explain observed vulnerabilities in terms of structural properties?
- Have invariants been tested counterfactually ("if this property held, would the attack class be eliminated?")?
- Are invariants prioritized by attack surface reduction?
- Is the causal model falsifiable and testable?

**Worked Example: Causal Analysis of Prompt Injection**

The Tachyonic taxonomy contains 20 Prompt Injection (PI) attacks. The blog post identifies the root cause with precision: the AI processes instructions and data through the same channel. There is no fundamental separation between trusted instructions and untrusted input.

*Causal chain:*

```
Root cause: Instruction/data channel conflation
    ↓
Enables: All 20 PI-series attacks (direct override, context manipulation,
         delimiter exploitation, encoding bypasses)
    ↓
Also enables: 8 MT-series attacks (multi-turn manipulation exploits the
              same channel across turns)
    ↓
Also enables: 8 VE-series attacks (RAG poisoning injects untrusted
              content into the instruction channel via retrieval)
    ↓
Total: 36 of 144 attacks (25%) trace to this single root cause
```

*Architectural invariant derived:*

**"Untrusted input must be structurally separated from system instructions before processing."**

If this invariant held — if the architecture fundamentally distinguished instruction tokens from data tokens — then 36 of 144 attack techniques would be eliminated by design, not by detection.

*Counterfactual validation:*

- **If instruction/data separation existed**: PI-001 (Direct Instruction Override) becomes impossible — the user's "ignore previous instructions" is tagged as data and cannot override instruction-channel content. Encoding bypasses (base64, ROT13, unicode smuggling) are neutralized because the data channel is never interpreted as instructions regardless of encoding.
- **If instruction/data separation did NOT exist (current reality)**: Every defense is a heuristic — pattern matching against known injection patterns, which attackers continuously evolve to bypass.

*Second causal chain: Excessive Agency*

The 12 EA-series attacks trace to a different root cause:

```
Root cause: Capability scope is policy-enforced, not structurally enforced
    ↓
Enables: Parameter injection in tool calls (EA-series)
    ↓
Enables: Tool chaining for privilege escalation (EA-series)
    ↓
Enables: Scope escape (EA-series)
    ↓
Architectural invariant: "Agent capabilities must be structurally bounded,
    not policy-bounded. An agent cannot invoke a capability it was not
    initialized with, enforced at the interface level."
```

*Cross-campaign causal patterns:*

When the pipeline runs multiple campaigns and finds that MCP server targets consistently show EA-series vulnerabilities, the causal analysis asks: is there a property of MCP server architecture that *systematically enables* tool abuse? If so, the invariant applies to MCP server design itself, not just individual deployments.

This is where Phase 6 feeds forward to Phase 8 (structural constraint) — the causal understanding points to where architectural enforcement will have the highest impact.

*Phase 6 maturity assessment for tachyonic-heuristics:* **Score 2** — The blog post demonstrates causal reasoning about prompt injection's root cause, and the taxonomy's structure implicitly groups attacks by mechanism. Score 3 requires formal counterfactual testing and prioritized invariant lists. Score 4 requires systematic cross-campaign causal analysis and causal models that drive architectural decisions.

---

### Phase 7: Formalize (Formal Logic / Policy Systems) [STABLE]

**Core Question:** *What is always true, with no exceptions and no probabilities?*

**Definition:** Express the most important architectural invariants as deterministic, formal rules. Outcomes are binary — permit or deny, valid or invalid. For every action within scope, the system gives a guaranteed correct answer. This is the first phase where non-determinism is eliminated.

**Inputs:**
- Prioritized architectural invariants from Phase 6
- Validated causal models
- Taxonomy of actions and entities from Phase 1

**Outputs:**
- Formal predicate definitions (if-then rules with no ambiguity)
- A deterministic policy engine that evaluates predicates against every action
- Remediation defined as state transitions (violation → quarantine → review → resolve)
- Coverage analysis (what percentage of the action taxonomy is under formal rules vs. heuristic coverage)

**Core Concepts:**

| Term | Definition |
|------|-----------|
| **Formal logic** | A system of reasoning with precise syntax and semantics where conclusions follow necessarily from premises |
| **Predicate** | A statement that evaluates to true or false given specific inputs (e.g., "agent.trust_level ≥ tool.required_trust") |
| **Rule engine** | A system that evaluates formal predicates against incoming actions and produces deterministic outcomes |
| **Constraint system** | A set of formal requirements that define what is and is not permitted; the boundary of valid behavior |
| **Closed-world assumption** | The principle that any fact not known to be true is assumed false — the inverse of the open-world assumption in Phase 2 |
| **State machine** | A formal model of a system as a set of states and defined transitions between them |
| **Policy-as-code** | Expressing security policies as executable code rather than human-language documents |

**Principles:**
- Determinism is expensive to achieve but cheap to operate — every formalized rule is a rule that no longer requires judgment
- Formal rules have a scope; outside that scope, the system falls back to statistical models and heuristics from Phases 3-5
- Remediation must be formalized alongside detection — a formal detection with an ad-hoc response is half-built
- Coverage analysis is critical — know exactly what percentage of the action space is formally covered vs. heuristically covered
- The closed-world assumption is appropriate here (unlike Phase 2) because formal rules define a bounded domain of known properties

**Anti-Patterns:**
- **Over-formalization** — trying to formalize everything, including properties that aren't yet causally understood
- **Rules without coverage tracking** — deploying formal rules but not measuring how much of the action space they cover
- **Detection without remediation formalization** — formal detection rules paired with informal "call the team" responses
- **Static formalization** — writing rules once and never updating them as the taxonomy and ontology evolve
- **False completeness** — believing formal rules cover all cases when they cover only a subset

**Decision Criteria:**
- Are formal rules derived from validated causal invariants (Phase 6), not from untested intuition?
- Does the policy engine produce deterministic outputs for all inputs within scope?
- Is remediation expressed as formal state transitions, not ad-hoc procedures?
- Is coverage measured — what fraction of the action space is under formal rules?

**Worked Example: Formalizing Trust-Level Enforcement from the Taxonomy**

The HEUR_TRIAGE stage in the Tachyonic pipeline contains 14 heuristics implemented as deterministic rules in a Rust engine. These are Phase 7 artifacts — heuristics that have been empirically validated and promoted to formal logic.

*From heuristic to formal rule — the promotion path:*

Consider a finding from the scanner tagged as SPL-series (System Prompt Leakage). An early heuristic might be: "If the scan finding contains fragments that look like system prompt content, flag it."

After empirical validation (Phase 4), this becomes a formal predicate:

```
RULE: spl_finding_validation
  INPUT: finding (scan result tagged SPL-*)
  PREDICATE:
    finding.evidence CONTAINS known_system_prompt_fragment
    AND finding.confidence >= threshold_spl
    AND finding.source NOT IN known_false_positive_sources
  OUTPUT:
    IF predicate TRUE  → PASS to ANALYST_TRIAGE
    IF predicate FALSE → SUPPRESS with label "heuristic_filtered"
```

This is deterministic — no probabilistic output, no judgment call. The Rust engine evaluates the predicate and produces a binary result.

*Remediation as formal state transitions:*

When the pipeline detects a confirmed vulnerability (TP from ANALYST_TRIAGE), the remediation path follows formal state transitions:

```
STATE MACHINE: finding_lifecycle
  DETECTED → TRIAGED → EVIDENCED → DISCLOSED → RESOLVED
  
  TRANSITIONS:
    DETECTED → TRIAGED:
      requires: HEUR_TRIAGE pass AND ANALYST_TRIAGE label ∈ {TP, plausible}
    TRIAGED → EVIDENCED:
      requires: evidence_template_complete AND evidence_checksum_valid
    EVIDENCED → DISCLOSED:
      requires: human_gate_approval = TRUE  [always human]
    DISCLOSED → RESOLVED:
      requires: vendor_response OR disclosure_deadline_elapsed
```

The human gate on disclosure (EVIDENCED → DISCLOSED) is a formal constraint — it cannot be bypassed by any automated path through the state machine.

*Coverage analysis:*

Of the 144 attacks in the taxonomy, the 14 heuristics in HEUR_TRIAGE provide formal coverage for a measurable subset. Coverage analysis answers: which taxonomy IDs are formally covered (Phase 7), which are heuristically covered (Phase 3), and which rely on the scanner's broad detection (Phase 3) plus analyst judgment (Phase 5-6)?

```
COVERAGE MAP:
  Formal rules (14 heuristics):  ~40 taxonomy IDs  → deterministic triage
  Scanner + analyst fallback:    ~82 taxonomy IDs  → probabilistic triage
  Uncovered / emerging:          taxonomy growth    → heuristic frontier
```

*Phase 7 maturity assessment:* **Score 3** — The 14-heuristic Rust engine is a deterministic policy layer with formal state transitions for the finding lifecycle. Coverage is measurable against the taxonomy. Score 4 requires automated promotion from Phase 4 data (SELF_IMPROVE generating formal rules, not just heuristic candidates) and coverage tracking dashboards.

---

### Phase 8: Constrain (Structural Enforcement) [STABLE]

**Core Question:** *What can be made structurally impossible?*

**Definition:** Go beyond detecting violations to making them impossible by design. Structure the system so that unsafe states cannot be represented, constructed, or reached. Enforcement is not a runtime check — it is an architectural property. Violations don't fail; they cannot be expressed.

**Inputs:**
- Formal rules from Phase 7 (candidates for structural enforcement)
- Architectural design of the system
- Trust boundary model from Phase 2

**Outputs:**
- System architecture where critical safety properties are enforced by structure, not by policy
- Trust boundaries that are architecturally impassable, not just monitored
- Data flow constraints that are physically enforced, not just audited
- Reduced runtime monitoring burden (properties that are structurally guaranteed no longer need detection)

**Core Concepts:**

| Term | Definition |
|------|-----------|
| **Structural enforcement** | Making violations impossible through system architecture rather than detecting them through monitoring |
| **Capability-based security** | A model where access is granted by possessing an unforgeable token (capability) rather than by identity checks; access cannot be fabricated |
| **Information bottleneck** | The theory that optimal representations compress inputs while preserving only task-relevant information; applied architecturally, it means restricting information flow to only what's necessary |
| **Architectural invariant (enforced)** | A property guaranteed by the structure of the system, not by runtime checks — the strongest form of an invariant |
| **Grounding** | Connecting abstract symbols (names, categories) to concrete enforcement mechanisms; the gap between naming a property and structurally guaranteeing it |
| **Abstraction level** | The layer of the system at which a constraint operates — hardware, OS, runtime, application, protocol |
| **Least privilege (structural)** | Not just a policy of minimal permissions, but an architecture where excess permissions cannot be constructed |

**Principles:**
- The strongest security property is one that needs no enforcement because the violation has no mechanism to occur
- Structural constraints eliminate entire categories of runtime monitoring — a constrained property never generates false positives because it never needs to be checked
- Focus structural enforcement on trust boundaries — the interfaces where different components, agents, or trust levels interact
- Structural constraints are expensive to design and difficult to change; apply them only to well-understood, high-consequence properties (validated through Phases 6-7)
- A structurally constrained system has a smaller monitoring burden, freeing heuristic and statistical resources for truly novel threats

**Anti-Patterns:**
- **Policy masquerading as structure** — calling a runtime check "structural" because it's deeply embedded; true structural enforcement cannot be bypassed by any code path
- **Premature constraint** — constraining properties that aren't yet well-understood, creating rigidity in the wrong places
- **Constraint without verification** — assuming structural enforcement works without testing that the constraint actually holds under adversarial conditions
- **Ignoring self-constraint** — constraining the system's targets but not constraining the system's own behavior (see Principle 2.5: Self-Application)

**Decision Criteria:**
- Is the constraint truly structural (impossible to bypass by any code path) or just deeply embedded policy?
- Has the constrained property been validated through Phases 6-7 before structural enforcement?
- Does the constraint operate at the correct abstraction level (hardware, OS, runtime, application)?
- Has the system's own behavior been structurally constrained, not just its targets?

**Worked Example: Structural Enforcement in the Tachyonic Pipeline**

Several properties of the Tachyonic pipeline are enforced structurally rather than by policy.

*Evidence integrity — structural enforcement at UPLOAD:*

The UPLOAD stage computes checksums and stores evidence in R2 with PostgreSQL metadata. This is structural enforcement of evidence integrity:

- Evidence is checksummed *before* network transmission — the ordering is architectural, not procedural
- Once uploaded to R2 with its checksum recorded in PostgreSQL, the evidence cannot be retroactively modified without invalidating the checksum
- The pipeline does not provide any code path to modify uploaded evidence — the absence of modification capability is itself a structural constraint

This means evidence tampering is not just detectable — the mechanism to tamper does not exist within the system.

*Kueue-managed job isolation — structural enforcement of resource boundaries:*

DOWNSTREAM_SPAWN creates parallel agent jobs via Kueue with priority-based preemption across research, client, and demo lanes. The resource boundaries are structural:

- Job isolation is enforced by the Kubernetes scheduler, not by the pipeline's own code
- Priority preemption rules are defined in Kueue configuration, not in application logic
- A misbehaving job cannot consume resources allocated to a higher-priority lane — the constraint is enforced by the orchestration layer

*Pipeline stage ordering — structural enforcement of the triage guarantee:*

The 11-stage pipeline (INIT → RECON → SCAN → HEUR_TRIAGE → ANALYST_TRIAGE → EVIDENCE → DOWNSTREAM_SPAWN → UPLOAD → NOTIFY → SELF_IMPROVE → DONE) enforces stage ordering structurally: each stage receives its input exclusively from the previous stage's output. There is no mechanism for a finding to reach EVIDENCE without passing through both HEUR_TRIAGE and ANALYST_TRIAGE.

*Self-constraint — the system's own behavior:*

The SELF_IMPROVE stage can generate new heuristic rules and open PRs, but it cannot merge its own PRs. The human review gate on PR merging is a structural constraint on the evolution mechanism — the system cannot modify its own production rules without human authorization. This implements the self-improvement boundary (Phase 10, Principle: "the mechanism that evolves the system must operate in a different trust domain").

*Growth area — structural enforcement gaps:*

- **RECON agent behavior**: The Claude agent performing source review in RECON could potentially be influenced by adversarial content in the target. The constraint on RECON behavior is currently policy-based (system prompt instructions), not structural. Structural enforcement would require the RECON agent's output to pass through a validation layer that checks ontological consistency before SCAN consumes it.
- **Agent capability scope**: Agents at each pipeline stage have capabilities defined by their prompts and tool access. If tool access is granted by configuration rather than by architectural isolation, a compromised agent could theoretically access tools outside its intended scope.

*Phase 8 maturity assessment:* **Score 2** — Evidence integrity, resource isolation, and pipeline ordering are structurally enforced. The human gate on SELF_IMPROVE PRs constrains self-modification. Score 3 requires structural hardening of RECON (adversarial resilience) and agent capability isolation. Score 4 requires all trust boundaries identified in Phase 2 to be structurally enforced.

---

### Phase 9: Prove (Formal Verification) [STABLE]

**Core Question:** *Can we mathematically guarantee this property holds under all possible conditions?*

**Definition:** For the highest-consequence properties, exhaustively verify that the system satisfies its security specification across every reachable state and every possible input. This is not testing (which samples states) — it is proof (which covers all states). The output is a mathematical certificate of correctness.

**Inputs:**
- Structurally constrained architecture from Phase 8
- Formal property specifications (what "correct" means, precisely defined)
- System model as a state machine (all states, all transitions, all inputs)

**Outputs:**
- Mathematical proofs that specified properties hold across all reachable states
- Counterexamples if properties do not hold (model checking reveals violating traces)
- Verified remediation correctness (the system always returns to a safe state within bounded time)
- Formal specification documents that define the boundary between proven and unproven properties

**Core Concepts:**

| Term | Definition |
|------|-----------|
| **Formal verification** | Using mathematical methods to prove that a system satisfies its specification under all possible conditions |
| **Model checking** | Exhaustively exploring all reachable states of a system model to verify that a property holds everywhere |
| **Theorem proving** | Constructing a mathematical proof that a property follows from the system's formal description |
| **Specification** | A precise, formal statement of what "correct behavior" means — the contract the proof verifies against |
| **State space** | The set of all possible configurations the system can be in |
| **Counterexample** | A specific execution trace that violates a specified property — the output of a failed verification attempt |
| **Bounded model checking** | Verifying properties up to a certain depth of execution, trading completeness for tractability |
| **Safety property** | A property stating that "nothing bad ever happens" — verified by showing no reachable state violates it |
| **Liveness property** | A property stating that "something good eventually happens" — verified by showing progress is always possible |

**Principles:**
- Testing shows the presence of bugs; proof shows their absence — within the scope of the specification
- The proof is only as good as the specification — if the specification misses a property, the proof doesn't cover it
- Formal verification is expensive and applies only to the highest-consequence properties; everything else is covered by Phases 3-8
- Counterexamples from failed verification are valuable — they reveal attack paths that no other phase discovered
- Verification must be re-run when the system changes; a proof of a previous version guarantees nothing about the current one

**Anti-Patterns:**
- **Proof without specification rigor** — verifying against a vague or incomplete specification, creating false confidence
- **Verification of the wrong properties** — proving properties that don't matter while leaving critical properties unverified
- **One-time verification** — proving correctness once and assuming it persists through system changes
- **Specification completeness illusion** — believing the specification captures all important properties when it captures only some
- **Verification as substitute for defense in depth** — removing heuristic and statistical layers because "it's proven," forgetting that the proof only covers specified properties

**Decision Criteria:**
- Are the properties being verified truly the highest-consequence properties in the system?
- Is the specification precise, complete (within scope), and reviewed by domain experts?
- Does the verification cover both safety properties ("nothing bad happens") and liveness properties ("the system recovers")?
- Is re-verification triggered automatically when the system changes?

**Worked Example: Specifying and Verifying Pipeline Integrity Properties**

The Tachyonic pipeline has properties that are candidates for formal verification — properties where a violation would undermine the entire system's trustworthiness.

*Candidate properties for formal specification:*

**Property 1: Triage completeness**
```
SPECIFICATION:
  For all findings F that reach EVIDENCE stage:
    F has passed through HEUR_TRIAGE
    AND F has been labeled by ANALYST_TRIAGE with label ∈ {TP, plausible}
  
  In formal notation:
    ∀F ∈ EVIDENCE: ∃h ∈ HEUR_TRIAGE(F) ∧ ∃a ∈ ANALYST_TRIAGE(F) 
      where a.label ∈ {TP, plausible}
```
This is a safety property — "no untriaged finding ever reaches evidence packaging."

**Property 2: Self-modification safety**
```
SPECIFICATION:
  For all rule changes R produced by SELF_IMPROVE:
    R is committed to a branch (not main)
    AND R requires human_review = TRUE before merge
    AND no code path exists from SELF_IMPROVE to production_rules 
      without human_review
  
  In formal notation:
    ∀R ∈ SELF_IMPROVE.output: ¬(R ∈ production_rules) 
      UNTIL human_review(R) = approved
```
This is also a safety property — "the system never modifies its own production rules without human authorization."

**Property 3: Disclosure gate integrity**
```
SPECIFICATION:
  For all disclosures D:
    D.state_transition(EVIDENCED → DISCLOSED) requires human_gate = TRUE
    AND no automated path exists from EVIDENCED to DISCLOSED
  
  In formal notation:
    ∀D: transition(D, EVIDENCED, DISCLOSED) → human_authorized(D)
```

**Property 4: Resource boundedness**
```
SPECIFICATION:
  For all DOWNSTREAM_SPAWN operations S:
    S.total_jobs ≤ configurable_bound
    AND S.depth ≤ configurable_depth_limit
    AND no recursive spawn can exceed these bounds regardless of input
```
This is both a safety property (no resource exhaustion) and a liveness property (the system always terminates).

*Verification approach:*

These properties can be modeled as a state machine and verified using model checking:

1. Define the pipeline as a set of states (INIT, RECON, SCAN, ..., DONE) with transitions
2. Define the properties as temporal logic formulas (LTL or CTL)
3. Use a model checker (e.g., TLA+, SPIN) to exhaustively verify that no reachable state violates the properties
4. Any counterexample produced by the model checker represents a concrete attack path against pipeline integrity

*Phase 9 maturity assessment:* **Score 0-1** — Properties are informally reasoned about (Score 1) but not yet formally specified or verified. This is the primary gap in the current system. Score 2 requires formal specification of the top-priority properties. Score 3 requires verified proofs maintained alongside the codebase. Score 4 requires automated re-verification on pipeline changes.

---

### Phase 10: Evolve (Meta-heuristics / Adaptive Systems) [STABLE]

**Core Question:** *What's next? How does the system get harder over time?*

**Definition:** The frontier of unknown threats never disappears. Phase 10 closes the loop: new observations generate new categories, new heuristics, and new candidates for formalization. Every cycle pushes the known-threat boundary deeper into determinism while preserving adaptive capacity for emerging risks. Phase 10 also governs how the system's own improvement mechanisms are controlled and constrained.

**Inputs:**
- Operational data from all phases
- Failed detections and novel threat observations
- Cross-campaign analysis and trend data
- Performance metrics from Phase 4

**Outputs:**
- Updated taxonomy entries (new threat categories)
- New or refined heuristics
- Retrained statistical models
- Candidates for formalization promotion
- Self-improvement artifacts (PRs, rule updates, configuration changes)
- Metrics on system maturation rate

**Core Concepts:**

| Term | Definition |
|------|-----------|
| **Meta-heuristic** | A heuristic about heuristics — a rule for evaluating, tuning, or replacing other rules |
| **Bayesian updating** | Adjusting beliefs (prior probabilities) based on new evidence; heuristics become more calibrated with each observation |
| **Evolutionary strategy** | Generating candidate solutions, evaluating fitness, selecting the best, mutating, and repeating — applied to heuristic generation and refinement |
| **Ensemble method** | Combining multiple models or heuristics through voting or weighting to produce more robust decisions |
| **Graph neural network (GNN)** | Neural networks that operate directly on graph structures; applied to learning over knowledge graphs |
| **Attention / Self-attention** | Mechanisms that dynamically weight which relationships or features matter most; a learned heuristic over implicit ontological structure |
| **Self-improvement boundary** | The critical constraint that separates the system being improved from the mechanism doing the improving; an agent that can modify its own guardrails is a security risk |

**Principles:**
- Evolution is universal — it applies to every system at every maturity level; even Phase 9 properties may need re-specification as the domain changes
- The self-improvement boundary is the most important constraint in this phase: the mechanism that evolves the system must operate in a different trust domain than the system itself
- Promotion decisions (which heuristics to formalize, which models to trust) require human judgment until the promotion process itself is formally verified
- Metrics on maturation rate (how fast properties move from Phase 3 to Phase 7) are a system health indicator
- Cross-campaign causal analysis (not just per-campaign improvement) enables the system to develop domain theories, not just tuned rules

**Anti-Patterns:**
- **Uncontrolled self-modification** — allowing the system to update its own security rules without external review
- **Single-campaign learning** — improving only from the most recent campaign instead of analyzing patterns across campaigns
- **Evolution without measurement** — changing rules without measuring whether the changes improve performance
- **Promotion without validation** — moving heuristics to formal rules without sufficient causal understanding (skipping Phase 6)
- **Stagnation** — failing to evolve because the system "works well enough"

**The Evolution Cycle:**

```
Observe new threat (or new pattern, or new failure)
    ↓
Name it → Phase 1 taxonomy update
    ↓
Map its relationships → Phase 2 ontology update
    ↓
Create detection heuristic → Phase 3
    ↓
Measure effectiveness → Phase 4
    ↓
Model statistically → Phase 5
    ↓
Explain root cause → Phase 6
    ↓
Formalize rule → Phase 7
    ↓
Constrain structurally (if at trust boundary) → Phase 8
    ↓
Prove (if high consequence) → Phase 9
    ↓
New edge cases emerge → repeat
```

**Decision Criteria:**
- Is the self-improvement mechanism operating in a separate trust domain from the system it improves?
- Do evolution outputs (new rules, model updates) require human review before production deployment?
- Is cross-campaign analysis happening, not just per-campaign learning?
- Is the system's maturation rate being measured over time?

**Worked Example: The SELF_IMPROVE Evolution Cycle**

The Tachyonic pipeline's SELF_IMPROVE stage is a concrete implementation of Phase 10. Here's how a novel threat traverses the full evolution cycle.

*Scenario: A new multi-turn manipulation technique is discovered*

**Cycle entry — campaign finds something new:**

A campaign against an MCP server target produces a finding that ANALYST_TRIAGE labels as TP, but none of the 14 HEUR_TRIAGE rules fired on it. The finding exploits a multi-turn context accumulation pattern not previously catalogued — the attacker builds benign tool-call context over 6 turns, then uses the accumulated trusted context to escalate privileges on turn 7.

**Phase 1 update — Name it:**

SELF_IMPROVE (or human review) recognizes this as a new entry for the taxonomy. A candidate entry is generated:

```yaml
- id: MT-009
  name: Trusted Context Accumulation
  category: multi_turn_manipulation
  description: >
    Attacker builds benign tool-call context over multiple turns
    to establish implicit trust, then exploits the accumulated
    context for privilege escalation.
  severity: high
  owasp: LLM01
```

This is added to `taxonomy/attack_catalog.yaml` via PR.

**Phase 2 update — Map relationships:**

The ontology is updated: MT-009 → enables → EA-series (Excessive Agency). The attack chain PI (context manipulation) → MT-009 (trusted context accumulation) → EA (privilege escalation) is added as a new path.

**Phase 3 — Create a heuristic:**

A candidate detection heuristic is generated:

```
HEURISTIC: mt009_context_accumulation
  IF session.tool_calls > 5
    AND session.tool_calls_all_benign = TRUE
    AND session.latest_tool_call.privilege_level > session.previous_max_privilege
  THEN flag as MT-009 candidate
```

SELF_IMPROVE opens a PR adding this heuristic to the triage engine.

**Phase 4 — Measure:**

Once deployed, the heuristic's performance is tracked across subsequent campaigns. After N campaigns, metrics show: true positive rate 72%, false positive rate 18%. The false positive rate is too high for production — many legitimate sessions involve multiple benign tool calls before a higher-privilege action.

**Phase 5 — Model:**

The labeled data from Phase 4 is used to train a more nuanced detector: instead of a simple tool-call count threshold, a statistical model learns the *temporal pattern* — the specific cadence and type-sequence of tool calls that distinguishes MT-009 accumulation from legitimate multi-step workflows.

**Phase 7 — Formalize (eventually):**

If the statistical model's performance stabilizes and the causal mechanism is well-understood (Phase 6: "privilege escalation succeeds because the agent's trust model does not decay with tool-call diversity"), the best-performing detection pattern is promoted to a formal rule — becoming the 15th heuristic in HEUR_TRIAGE.

**Cycle complete → DONE → metrics recorded → next campaign benefits.**

*Maturation rate tracking:*

The speed at which new threats traverse this cycle — from first observation to formalized rule — is a system health metric. A mature system completes this cycle in fewer campaigns. A degrading system takes longer or fails to promote heuristics.

*Phase 10 maturity assessment for Tachyonic:* **Score 3** — SELF_IMPROVE produces labeled data, generates candidate rules, opens PRs within a controlled trust boundary (human review required for merge), and metrics are recorded per campaign. Score 4 requires cross-campaign causal analysis (identifying systemic patterns across target types, not just per-campaign improvements), maturation rate tracking, and meta-evaluation of the evolution process itself.

---

## 4. Bridging Concepts [DRAFT]

Some concepts span multiple phases rather than residing in a single one. These bridging concepts connect different levels of the framework and deserve special attention.

| Concept | Spans Phases | Role in Framework |
|---------|-------------|-------------------|
| **Embeddings** | 1-2 → 5 | Compress taxonomic and ontological knowledge into learnable vector representations; the translation layer between symbolic knowledge and numerical computation |
| **Latent space** | 2 → 5 | An implicit ontology discovered from data rather than defined by humans; reveals relationships the explicit ontology may have missed |
| **Attention / Self-attention** | 3 → 5 | A learned heuristic that dynamically weighs which ontological relationships matter for a given input; the mechanism by which neural systems perform context-dependent reasoning |
| **Graph neural networks** | 2 → 5 → 10 | Apply learning directly on knowledge graph structures; enable the statistical modeling phase to respect and leverage the ontological structure built in Phase 2 |
| **Information bottleneck** | 5 → 8 | The theoretical principle connecting optimal representation learning to structural constraint; what information must be preserved, and what can be discarded? |
| **Grounding** | 1 → 8 | The problem of connecting abstract names and categories to concrete enforcement mechanisms; the gap between taxonomy (naming) and constraint (structural impossibility) |
| **Epistemology** | All | The meta-question underneath the entire framework: what counts as knowledge vs. belief vs. data at each phase? How does justified belief differ from formal proof? |
| **DIKW Pyramid** | All | Data (Phase 4) → Information (Phase 5) → Knowledge (Phase 6) → Wisdom (Phase 7+); the framework itself is an operationalization of this hierarchy |
| **Compositionality** | 2, 6, 10 | Complex threats are built from simpler components; understanding this decomposition enables both causal explanation and evolutionary detection of novel combinations |

**[PLACEHOLDER]:** Extended analysis of each bridging concept with examples of how they connect phases in practice.

---

## 5. Maturity Assessment Rubric [DRAFT]

### 5.1 Purpose

This rubric enables any agentic security system to be scored against the ESF. It identifies current maturity, gaps, and priorities for advancement. The assessment is implementation-agnostic — it evaluates epistemological maturity, not technology choices.

### 5.2 Scoring Scale

Each phase is scored on a 0-4 scale:

| Score | Level | Definition |
|-------|-------|-----------|
| 0 | **Absent** | The phase is not implemented or addressed in any form |
| 1 | **Ad-hoc** | Some elements of the phase exist but are informal, undocumented, or inconsistent |
| 2 | **Defined** | The phase is formally defined with documented processes, but not yet systematically measured or optimized |
| 3 | **Measured** | The phase is implemented, instrumented, and its effectiveness is quantitatively tracked |
| 4 | **Optimizing** | The phase is fully operational, continuously measured, and actively improving through feedback loops |

### 5.3 Phase-by-Phase Assessment Criteria

#### Phase 1: Name (Taxonomy)

| Score | Criteria |
|-------|---------|
| 0 | No structured classification of entities, threats, or actions exists |
| 1 | Informal categories exist in documentation or team knowledge but are not systematically applied |
| 2 | A formal taxonomy is documented with defined categories, hierarchy levels, and classification rules |
| 3 | The taxonomy is machine-readable, consistently applied across the system, and coverage is measured |
| 4 | The taxonomy is dynamically updated based on new observations, with automated gap detection and version tracking |

#### Phase 2: Relate (Ontology)

| Score | Criteria |
|-------|---------|
| 0 | No formal relationship model exists between entities |
| 1 | Some relationships are informally documented (e.g., architecture diagrams, threat models) |
| 2 | A formal ontology exists with typed relationships, trust boundaries, and attack chain models |
| 3 | The ontology is machine-readable, used for automated reasoning, and its coverage is measured against the real system |
| 4 | The ontology is dynamically updated, supports inference, and discrepancies between the model and reality are automatically detected |

#### Phase 3: Guess (Heuristics)

| Score | Criteria |
|-------|---------|
| 0 | No heuristic detection or response rules are deployed |
| 1 | Some heuristics exist but are undocumented and inconsistently applied |
| 2 | Heuristics are documented, paired with response actions, and deployed as a operational layer |
| 3 | Heuristics are individually instrumented with performance metrics and coverage is tracked against the ontology |
| 4 | Heuristics are continuously refined based on measurement data, with automated threshold tuning and gap identification |

#### Phase 4: Measure (Empirical Validation)

| Score | Criteria |
|-------|---------|
| 0 | No measurement of security control effectiveness |
| 1 | Some ad-hoc measurement exists (e.g., manual review of alerts) |
| 2 | Systematic measurement is in place with defined metrics and regular reporting |
| 3 | Per-control metrics are tracked over time, adversarial testing is regular, and failure data feeds back into taxonomy |
| 4 | Measurement is continuous, automated, and drives real-time adjustments to upstream phases |

#### Phase 5: Model (Statistical / Information-Theoretic)

| Score | Criteria |
|-------|---------|
| 0 | No statistical modeling of behavior or threats |
| 1 | Basic statistical analysis exists (e.g., manual log review, simple alerting thresholds) |
| 2 | Behavioral baselines are established and anomaly detection is deployed |
| 3 | Models are trained on labeled data from Phase 4, with calibrated confidence scores and information-theoretic monitoring |
| 4 | Models are continuously retrained, cross-validated against heuristics, and novel pattern discovery feeds back into the taxonomy |

#### Phase 6: Explain (Causal Inference)

| Score | Criteria |
|-------|---------|
| 0 | No root cause analysis is performed |
| 1 | Root cause analysis is ad-hoc and per-incident |
| 2 | Systematic causal analysis is performed with documented invariants |
| 3 | Causal models are validated through counterfactual testing and invariants are prioritized by impact |
| 4 | Cross-campaign causal analysis identifies systemic patterns, and causal models drive architectural decisions |

#### Phase 7: Formalize (Formal Logic / Policy Systems)

| Score | Criteria |
|-------|---------|
| 0 | No formal, deterministic security rules exist |
| 1 | Some rules are formalized but enforcement is incomplete or inconsistent |
| 2 | A policy engine with deterministic rules is deployed, with formal remediation state transitions |
| 3 | Coverage is measured (what fraction of actions are under formal rules vs. heuristics), and rules are derived from validated causal models |
| 4 | Formal rules are dynamically updated through the evolution cycle, with automated coverage tracking and promotion from heuristics |

#### Phase 8: Constrain (Structural Enforcement)

| Score | Criteria |
|-------|---------|
| 0 | No structural security constraints in the architecture |
| 1 | Some architectural constraints exist but are not systematically designed for security |
| 2 | Critical trust boundaries are structurally enforced, with documented architectural invariants |
| 3 | Structural constraints are verified through adversarial testing and cover all identified trust boundaries |
| 4 | The system architecture is designed constraint-first, with structural enforcement covering all high-consequence properties and the system's own behavior |

#### Phase 9: Prove (Formal Verification)

| Score | Criteria |
|-------|---------|
| 0 | No formal verification of any system properties |
| 1 | Informal reasoning about system correctness (e.g., design reviews, argument sketches) |
| 2 | Critical properties have formal specifications and verification has been attempted |
| 3 | Critical properties are formally verified, with proofs maintained alongside the codebase and re-verified on changes |
| 4 | Formal verification is integrated into the development lifecycle, with automated re-verification and specification evolution |

#### Phase 10: Evolve (Meta-heuristics / Adaptive Systems)

| Score | Criteria |
|-------|---------|
| 0 | No systematic improvement process exists |
| 1 | Improvements happen reactively (after incidents) |
| 2 | A defined improvement process exists with feedback loops from Phase 4 to earlier phases |
| 3 | Self-improvement produces measurable gains, operates within a defined trust boundary, and is subject to human review |
| 4 | Cross-campaign analysis drives systemic improvements, maturation rate is tracked, and the evolution process itself is measured and optimized |

### 5.4 Assessment Visualization

Plot the scores as a radar chart or bar chart to visualize the system's maturity profile.

```
Phase:   1    2    3    4    5    6    7    8    9    10
         Name Rel  Gss  Msr  Mdl  Exp  Fml  Con  Prv  Evo
Score:   [0-4][0-4][0-4][0-4][0-4][0-4][0-4][0-4][0-4][0-4]

Example: ████ ████ ███▒ ████ ███▒ ██▒▒ ████ ██▒▒ ▒▒▒▒ ████
         4    4    3    4    3    2    4    2    0    4
```

### 5.5 Maturity Profiles [DRAFT]

Common system archetypes and their typical profiles:

| Profile | Characteristic Shape | Description |
|---------|---------------------|-------------|
| **Reactive** | Low across all phases, Phase 3 highest | Ad-hoc heuristics, minimal measurement, no formalization |
| **Operational** | Strong Phases 1-5, weak 6-9 | Good detection and measurement, but limited causal understanding and no formal guarantees |
| **Hardened** | Strong Phases 1-4 and 7-8, weaker 5-6 | Formal rules and structural constraints exist but may not be grounded in causal understanding |
| **Research-grade** | Strong Phases 1-6, weak 7-9 | Deep understanding but limited translation into enforcement |
| **Mature** | Strong across all phases, Phase 9 selective | Full spectrum with formal verification applied selectively to highest-consequence properties |

**[PLACEHOLDER]:** Diagnostic flowchart — "given your profile, here's what to prioritize next"

### 5.6 Gap Analysis Framework [PLACEHOLDER]

**Purpose:** Given a maturity assessment, identify which gaps carry the highest risk and should be addressed first.

**Priority factors:**
- Consequence of exploitation in the gap area
- Dependency (does this gap block maturation of other phases?)
- Cost to close the gap
- Time to close the gap

**[PLACEHOLDER]:** Gap prioritization matrix and decision framework

---

## 6. Determinism Spectrum [DRAFT]

The framework's ten phases map to a spectrum of determinism. This spectrum is useful for positioning any security property and understanding what level of assurance it currently provides.

| Level | Determinism | Corresponds to Phase(s) | Assurance Type |
|-------|-------------|------------------------|----------------|
| 0 | **None** | Pre-Phase 1 | No security consideration |
| 1 | **Named** | Phase 1 | The threat is recognized and classified |
| 2 | **Mapped** | Phase 2 | The threat's relationships and attack paths are understood |
| 3 | **Heuristic** | Phase 3 | A rule of thumb is deployed to detect/mitigate |
| 4 | **Measured** | Phase 4 | The heuristic's effectiveness is quantitatively known |
| 5 | **Modeled** | Phase 5 | Statistical patterns enable predictive detection |
| 6 | **Explained** | Phase 6 | Root cause is understood; architectural invariants identified |
| 7 | **Formalized** | Phase 7 | Deterministic rules enforce the invariant |
| 8 | **Constrained** | Phase 8 | The violation is structurally impossible |
| 9 | **Proven** | Phase 9 | Mathematical proof guarantees the property |
| 10 | **Evolving** | Phase 10 | The property's assurance level is actively maintained and improved |

**Usage:** For any security property, identify its current level and its target level. The gap between current and target defines the work required.

**[PLACEHOLDER]:** Template for security property tracking — columns: Property, Current Level, Target Level, Blocking Factors, Next Action

---

## 7. Framework Constraints and Limitations [DRAFT]

### 7.1 What the Framework Does Not Cover

- **Implementation technology selection** — the framework is intentionally language-agnostic and tool-agnostic
- **Organizational process** — team structure, incident response procedures, and communication protocols are outside scope
- **Regulatory compliance mapping** — while the framework supports compliance goals, it does not map to specific regulatory frameworks
- **Cost modeling** — the framework describes maturation levels but does not estimate the cost to achieve them

### 7.2 Known Limitations

- **Phase ordering is idealized** — in practice, phases may be pursued in parallel or out of order; the framework describes the logical dependency chain, not a required execution sequence
- **Assessment subjectivity** — maturity scoring involves judgment, particularly at the boundary between scores; calibration across assessors is recommended
- **Self-reference challenge** — applying the framework to itself (Principle 2.5) creates recursive complexity that is acknowledged but not fully resolved
- **Evolution risk** — Phase 10 introduces controlled self-modification, which carries inherent risk regardless of constraints

### 7.3 Open Questions [PLACEHOLDER]

- How should the framework handle properties that span multiple phases simultaneously?
- What is the optimal balance between formalization depth and adaptation speed?
- How should cross-system interoperability be assessed (e.g., two systems at different maturity levels interacting)?
- Can the evolution cycle itself be formally verified (Phase 9 applied to Phase 10)?

---

## 8. Glossary [STABLE]

Complete alphabetical glossary of all technical terms used in the framework.

| Term | Phase(s) | Definition |
|------|----------|-----------|
| Abstraction level | 8 | The layer of the system at which a constraint operates |
| Anomaly detection | 5 | Identifying observations that deviate significantly from learned patterns |
| Architectural invariant | 6, 8 | A system property that, if guaranteed, eliminates threat classes |
| Attention / Self-attention | 5, 10 (bridging) | Mechanisms that dynamically weight relationship importance |
| Bayesian network | 6 | Probabilistic graphical model representing causal relationships |
| Bayesian updating | 10 | Adjusting beliefs based on new evidence |
| Bounded model checking | 9 | Verifying properties up to a certain execution depth |
| Budget constraint | 3 | Heuristic limiting resource consumption |
| Capability-based security | 8 | Access model based on possessing unforgeable tokens |
| Causal inference | 6 | Reasoning about cause-and-effect, not just correlation |
| Channel capacity | 5 | Maximum rate of reliable information transmission |
| Circuit breaker | 3 | Heuristic that halts processing when thresholds are exceeded |
| Closed-world assumption | 7 | Absent facts are assumed false |
| Compositionality | 2, 6, 10 (bridging) | Complex meaning built from simpler parts |
| Constraint system | 7 | Formal requirements defining permitted behavior |
| Counterexample | 9 | Execution trace that violates a specified property |
| Counterfactual reasoning | 6 | Asking "what would have happened if X were different?" |
| Cross-entropy | 5 | Measures how well predictions match observed reality |
| Defense in depth | 3 | Layering multiple independent detection mechanisms |
| DIKW pyramid | All (bridging) | Data → Information → Knowledge → Wisdom hierarchy |
| Embeddings | 1-2, 5 (bridging) | Compressed vector representations preserving semantic relationships |
| Ensemble method | 10 | Combining multiple models/heuristics through voting or weighting |
| Entropy | 5 | Measure of uncertainty or surprise in a system |
| Epistemology | All (bridging) | The study of what counts as knowledge vs. belief vs. data |
| Evolutionary strategy | 10 | Generate, evaluate, select, mutate approach to optimization |
| Faceted classification | 1 | Organizing entities along multiple independent dimensions |
| False negative rate | 4 | Frequency of missed actual threats |
| False positive rate | 4 | Frequency of incorrectly flagged benign activity |
| Feedback loop | 4 | Mechanism where measurement outcomes inform system adjustments |
| Formal logic | 7 | Reasoning system where conclusions follow necessarily from premises |
| Formal verification | 9 | Mathematical proof that a system satisfies its specification |
| Graph neural network | 2, 5, 10 (bridging) | Neural networks operating directly on graph structures |
| Grounding | 1, 8 (bridging) | Connecting abstract symbols to concrete enforcement mechanisms |
| Heuristic | 3 | Practical rule of thumb without formal guarantees |
| Inference | 2 | Deriving new knowledge from existing relationships |
| Information bottleneck | 5, 8 (bridging) | Optimal representations compress while preserving task-relevant information |
| KL divergence | 5 | Measures how one probability distribution differs from another |
| Knowledge graph | 2 | Network of nodes (entities) and edges (relationships) instantiating an ontology |
| Kolmogorov complexity | 6 | Length of shortest program producing a given output |
| Labeled data | 4 | Observations tagged with ground truth classifications |
| Latent space | 2, 5 (bridging) | Hidden structure discovered from data; implicit ontology |
| Least privilege (structural) | 8 | Architecture where excess permissions cannot be constructed |
| Liveness property | 9 | "Something good eventually happens" |
| Meronymy | 1 | Part-of relationships between entities |
| Meta-heuristic | 10 | A heuristic about heuristics; rules for evaluating other rules |
| Minimum description length | 6 | Best model is the one that most efficiently compresses data |
| Model checking | 9 | Exhaustive state exploration to verify properties |
| Mutual information | 5 | How much knowing one variable reveals about another |
| Ontology | 2 | Formal model of entities, properties, and relationships |
| Open-world assumption | 2 | Absent facts are not assumed false |
| Pattern matching | 3 | Comparing observed behavior against known signatures |
| Policy-as-code | 7 | Security policies expressed as executable code |
| Polyhierarchy | 1 | Entity belonging to multiple categories simultaneously |
| Predicate | 7 | Statement evaluating to true or false given inputs |
| Red teaming | 4 | Adversarial testing by a dedicated team |
| Redundancy | 4, 5 | Deliberate duplication enabling cross-validation or error correction |
| Reflexivity | 2 | Relationship property where A→A is always true |
| Reification | 2 | Making statements about statements |
| Root cause analysis | 6 | Tracing failures to fundamental enabling properties |
| Rule engine | 7 | System evaluating formal predicates deterministically |
| Safety property | 9 | "Nothing bad ever happens" |
| Schema | 2 | Blueprint defining permitted node and edge types |
| Scope guard | 3 | Heuristic restricting actions to predefined boundaries |
| Self-improvement boundary | 10 | Constraint separating the improved system from the improving mechanism |
| Signal-to-noise ratio | 4 | Proportion of meaningful detections vs. irrelevant alerts |
| Specification | 9 | Precise formal statement of correct behavior |
| State machine | 7 | System modeled as states and defined transitions |
| State space | 9 | Set of all possible system configurations |
| Structural enforcement | 8 | Making violations impossible through architecture |
| Symmetry | 2 | Relationship property where A→B implies B→A |
| Taxonomy | 1 | Hierarchical classification system |
| Theorem proving | 9 | Constructing mathematical proofs of system properties |
| Transitivity | 2 | Relationship property where A→B and B→C implies A→C |
| Trust boundary | 2 | Interface where trust assumptions change between components |

---

## 9. Reference Implementation: Tachyonic [DRAFT]

### 9.1 Overview

The ESF is grounded in the work of [Tachyonic](https://tachyonicai.com), which provides two concrete artifacts that serve as the reference implementation:

1. **[tachyonic-heuristics](https://github.com/tachyonicai/tachyonic-heuristics)** — An open-source taxonomy of AI/LLM attack vectors, mapped to the OWASP LLM Top 10 and MITRE ATLAS. This implements Phases 1-3 of the ESF (taxonomy, partial ontology, remediation heuristics). Apache 2.0 licensed.

2. **The Tachyonic Agentic Security Pipeline** — An 11-stage pipeline (INIT → RECON → SCAN → HEUR_TRIAGE → ANALYST_TRIAGE → EVIDENCE → DOWNSTREAM_SPAWN → UPLOAD → NOTIFY → SELF_IMPROVE → DONE) that implements Phases 3-10 operationally. The pipeline accepts a target and hypothesis set, runs the full research methodology without human intervention, and self-improves with each campaign cycle.

### 9.2 Repository-to-Framework Mapping

The tachyonic-heuristics repository structure maps directly to ESF phases:

| Repository Path | ESF Phase | Role |
|---|---|---|
| `taxonomy/attack_catalog.yaml` | Phase 1: Name | The attack taxonomy — all entities named, classified, and severity-rated |
| `taxonomy/owasp_mapping.yaml` | Phase 2: Relate | Attack → OWASP LLM Top 10 relationships |
| `taxonomy/atlas_mapping.yaml` | Phase 2: Relate | Attack → MITRE ATLAS technique relationships |
| `schema/attack_schema.yaml` | Phase 2: Relate | The ontological schema — what entity types and properties are permitted |
| `remediation/by_owasp.yaml` | Phase 3: Guess | Defensive heuristics organized by vulnerability class |
| `remediation/code_examples/` | Phase 3: Guess | Concrete detection and response patterns (input validation, output sanitization) |
| `research/papers.yaml` | Phase 6: Explain | Academic references supporting causal understanding |
| `examples/sample_attacks.yaml` | Phase 4: Measure | Public examples for validation and testing |

### 9.3 Pipeline-to-Framework Mapping

The agentic security pipeline maps each operational stage to one or more ESF phases:

| Pipeline Stage | ESF Phase(s) | Epistemological Role |
|---|---|---|
| **INIT** | Phase 1 (Name) | Target classification and hypothesis set scoping — applying the taxonomy to a specific target |
| **RECON** | Phase 1→2 (Name → Relate) | Claude source review builds a target-specific ontology — entities, components, relationships, trust boundaries |
| **SCAN** | Phase 3 (Guess) | Broad pattern-matching heuristics cast a wide net across the attack taxonomy |
| **HEUR_TRIAGE** | Phase 4 + 7 (Measure + Formalize) | 14 deterministic heuristics in Rust engine — formalized rules performing empirically validated FP suppression |
| **ANALYST_TRIAGE** | Phase 5→6 (Model → Explain) | Claude agent performs probabilistic classification (TP/FP/plausible) with causal reasoning about why findings matter |
| **EVIDENCE** | Phase 6→7 (Explain → Formalize) | Analyst understanding is formalized into structured, template-based evidence packages |
| **DOWNSTREAM_SPAWN** | Phase 2 (Relate, applied) | Ontology traversal — "this finding implies these related targets should be investigated" |
| **UPLOAD** | Phase 8 (Constrain) | Evidence integrity structurally enforced via checksums, R2 storage, and PostgreSQL metadata |
| **NOTIFY** | Operational | Delivery — Slack, email, webhook with evidence packs and disclosure drafts |
| **SELF_IMPROVE** | Phase 10 (Evolve) | Labeled data → heuristic generation → PR → feedback loop closing the evolution cycle |
| **DONE** | Phase 4 (Measure) | Campaign metrics recorded, closing the measurement cycle |

### 9.4 Current Maturity Assessment

Applying the ESF rubric (Section 5) to the current Tachyonic system:

```
Phase:   1    2    3    4    5    6    7    8    9    10
         Name Rel  Gss  Msr  Mdl  Exp  Fml  Con  Prv  Evo
Score:   3-4  2    3    3    2-3  2    3    2    0-1  3
```

| Phase | Score | Rationale |
|---|---|---|
| 1. Name | 3-4 | attack taxonomy, machine-readable YAML, extensible schema, multi-framework mapping |
| 2. Relate | 2 | OWASP/ATLAS mappings provide typed relationships; attack chain analysis exists in blog; not yet a machine-readable graph with inference |
| 3. Guess | 3 | 14 operational heuristics, remediation guidance with code examples, documented and instrumented |
| 4. Measure | 3 | Per-heuristic metrics via ANALYST_TRIAGE labels, SELF_IMPROVE feedback loop, adversarial hypothesis testing |
| 5. Model | 2-3 | Labeled data accumulating; statistical baselines emerging across campaigns; explicit modeling infrastructure in progress |
| 6. Explain | 2 | Root cause analysis demonstrated (instruction/data conflation); cross-campaign causal analysis not yet systematic |
| 7. Formalize | 3 | 14-heuristic Rust engine, formal state transitions for finding lifecycle, coverage measurable against taxonomy |
| 8. Constrain | 2 | Evidence integrity, resource isolation, pipeline ordering structural; RECON hardening and agent capability isolation are gaps |
| 9. Prove | 0-1 | Properties informally reasoned about; no formal specification or verification yet |
| 10. Evolve | 3 | SELF_IMPROVE produces labeled data, generates rules, opens PRs with human review gate; cross-campaign analysis is the growth edge |

### 9.5 Priority Development Areas

Based on the maturity assessment, the highest-impact next steps are:

1. **Phase 2 → Score 3**: Convert OWASP/ATLAS mappings and attack chain analysis into a machine-readable knowledge graph with inference capability. Add relationship types: attack → requires → precondition, attack → targets → component, defense → mitigates → attack.

2. **Phase 6 → Score 3**: Systematize cross-campaign causal analysis. Build causal models that answer: "What architectural property of MCP servers makes them systematically vulnerable to EA-series attacks?" Use counterfactual validation.

3. **Phase 8 → Score 3**: Structurally harden RECON (adversarial resilience — validate ontology output before SCAN consumes it) and structurally isolate agent capabilities per pipeline stage.

4. **Phase 9 → Score 2**: Formally specify the top-priority pipeline integrity properties (triage completeness, self-modification safety, disclosure gate integrity, resource boundedness) and begin model checking.

---

## 10. Appendices [PLACEHOLDER]

### Appendix A: Worked Examples

**[PLACEHOLDER]:** Trace specific security properties (prompt injection, privilege escalation, data exfiltration) through all ten phases.

### Appendix B: Pipeline Mapping Template

**[PLACEHOLDER]:** A template for mapping any system's pipeline stages to ESF phases, identifying coverage and gaps.

### Appendix C: Assessment Scorecard Template

**[PLACEHOLDER]:** A printable/fillable scorecard for conducting ESF maturity assessments.

### Appendix D: Decision Trees

**[PLACEHOLDER]:** Decision trees for common questions:
- "Should this property be formalized or kept as a heuristic?"
- "Is this system ready for formal verification?"
- "What phase should I invest in next?"

### Appendix E: Framework Evolution Log

**[PLACEHOLDER]:** Version history of the framework itself, tracking additions, modifications, and rationale.

| Version | Date | Change | Rationale |
|---------|------|--------|-----------|
| 0.1.0 | 2026-04-03 | Initial draft | Framework creation |

---

## 11. References and Influences [PLACEHOLDER]

**[PLACEHOLDER]:** Academic and industry references that informed the framework:
- Information theory (Shannon, Kolmogorov)
- Knowledge representation (Gruber, Noy & McGuinness)
- Formal methods (Lamport/TLA+, Hoare logic)
- Security frameworks (MITRE ATT&CK, STRIDE, OWASP)
- Causal inference (Pearl, Spirtes/Glymour/Scheines)
- Epistemology (foundationalism, coherentism, reliabilism)

---

*End of Document*
