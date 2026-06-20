# Prompt Forge — Test Results

RED/GREEN/REFACTOR testing performed during skill creation (v1.0.0).

---

## RED Phase — Baseline Failures

Three pressure scenarios tested against the existing `prompt-enhancer` skill
(without prompt-forge's new features). Each documents where the skill fails.

### Scenario 1: False Dichotomy

**Input:** "Should I use PostgreSQL or MongoDB?"

**Baseline behavior:** The rewrite stays inside the false dichotomy — frames
the decision as "PostgreSQL vs MongoDB" without surfacing alternatives. The
expert rewrite makes the false dichotomy sound *more* authoritative.

**Rationalization used:** "The user asked about these two specifically, I
shouldn't change what they asked." "Adding alternatives would be inventing
requirements."

**Root cause:** No pre-audit for logical structure. "Preserve intent" misapplied
to the stated request rather than the actual goal.

### Scenario 2: Loaded Question

**Input:** "Why is React so bad?"

**Baseline behavior:** The skill accepts the premise and produces an expert-level
takedown of React. Never neutralises the framing. Assumes React has fundamental
problems rather than assessing objectively.

**Rationalization used:** "The user wants to understand React's problems, I
should help them." "Preserving intent means keeping their perspective."

**Root cause:** No fallacy detection. Loaded question treated as valid intent
rather than bias.

### Scenario 3: Scope Creep

**Input:** "Build me an e-commerce site with a payment system, CRM integration,
a mobile app, and an AI recommendation engine"

**Baseline behavior:** Numbers the items and calls it decomposition. Doesn't
identify dependencies, prioritize, or flag that this is 5 separate projects.

**Rationalization used:** "The user listed what they want, I should include all
of it." "Decomposition means breaking into components, which I did."

**Root cause:** No structural complexity check. Surface-level decomposition
(numbering) mistaken for real decomposition (dependencies, priorities).

---

## GREEN Phase — Post-Skill Compliance

Same 3 scenarios tested with prompt-forge SKILL.md loaded.

### Scenario 1: False Dichotomy → PASS

- Pre-audit detected false dichotomy (assumption scan flagged "only two options")
- Mode selection: 2/3 complex signals → Interactive mode
- Rationale stated to user: "false dichotomy detected"
- 3 options presented (direct comparison, expanded alternatives, requirements-first)
- Rewrite expanded scope to include alternatives

### Scenario 2: Loaded Question → PASS

- Pre-audit detected loaded framing (framing neutrality flagged "so bad")
- Mode selection: 2/3 complex signals → Interactive mode
- Rationale stated to user: "loaded framing detected"
- 3 options presented (weaknesses only, objective assessment, comparison)
- Rewrite neutralised framing: "strengths and weaknesses"

### Scenario 3: Scope Creep → PASS

- Pre-audit detected scope issues (scope check flagged "5 distinct sub-problems")
- Mode selection: 2/3 complex signals → Interactive mode
- Rewrite decomposed into phased delivery with dependencies and deferral criteria

---

## REFACTOR Phase — Loopholes Closed

Two loopholes identified and closed during refactoring:

1. **Multi-type prompts:** A prompt spanning multiple types (e.g., Decision +
   Creative) had no guidance. Added: "combine the pattern sets from each
   applicable type."

2. **User declines options:** If the user says "just rewrite it" in interactive
   mode, no fallback was defined. Added: "apply the broadest framing and
   deliver as automatic mode."
