---
name: prompt-forge
description: |
  Use when user asks to improve, refine, or rewrite a prompt for an AI system,
  or when framing a request that feels vague, overloaded, or logically unsound.
  Triggers: "improve my prompt", "rewrite this prompt", "make this prompt better",
  "help me ask this question properly", "this prompt feels off".
---

# Prompt Forge

Transform novice prompts into expert-framed requests with logical rigor.
Preserve intent. Fix structure. Never amplify a flawed premise.

## When to Use

```
User provides a prompt to improve
  ├─ Pre-audit passes + simple structure → Automatic mode (single rewrite)
  └─ Pre-audit flags issues OR complex structure → Interactive mode (options + rationale)
```

- User asks to improve/refine/rewrite a prompt
- A prompt feels vague, overloaded, or logically unsound
- User needs help framing a request for an AI system

## When NOT to Use

- Prompts that are already expert-level (pass through with minor tweaks)
- Prompts for non-NLP systems (code generation, data processing pipelines)
- User explicitly says "don't change my wording"
- Single-word or trivially short prompts ("translate this", "summarize")

## Quick Reference

### Expert Communication Patterns

| Pattern | Novice | Expert |
|---------|--------|--------|
| Precision | "make it faster" | "optimise page load performance" |
| Decomposition | Single vague request | Logical components with dependencies |
| Constraints | Unstated | Explicit limits, trade-offs, success criteria |
| Context | Missing | System fit, standards, prior attempts |
| Role framing | None | "As a database architect, review this schema" |
| Failure modes | Ignored | Anticipated and specified |

### Prompt Classification Router

| Type | Trigger words | Apply patterns | Skip |
|------|--------------|----------------|------|
| Informational | explain, describe, what is | precision, context, audience | failure modes |
| Creative | write, design, compose | constraints, aesthetic direction | decomposition (unless complex) |
| Analytical | evaluate, compare, assess | decomposition, framework, success criteria | role framing |
| Action | fix, implement, optimise | decomposition, failure modes, constraints | context (if clear) |
| Decision | choose, recommend, should I | all patterns + reasoning cues | none |

### Fallacy Detection

| Fallacy | Detection | Correction |
|---------|-----------|------------|
| False dichotomy | "X or Y?" with no Z | Expand: "Evaluate X, Y, and alternatives" |
| Loaded question | "Why is X bad?" | Neutralise: "Assess X — strengths and weaknesses" |
| Premature conclusion | "Fix the bug" (unverified) | Reframe: "Investigate whether X has a defect" |
| Scope creep | 3+ unrelated asks in one prompt | Decompose + prioritise |
| Anchoring | "X costs $Y" (unverified) | Remove anchor: "Determine cost of X" |
| Survivorship bias | "What do successful people do?" | Add: "What do unsuccessful people do differently?" |

### Mode Selection Logic

Three signals evaluated in sequence:

| Signal | "Complex" threshold |
|--------|-------------------|
| 1. Classification | Decision or Analytical type |
| 2. Pre-audit | Any fallacy or ambiguity detected |
| 3. Structure | 2+ sub-problems OR multi-domain |

**Rule:** 2+ signals trigger "complex" → Interactive mode. Otherwise → Automatic.

**Interactive output:** State the decision + rationale before presenting options.
Example: "Processing in interactive mode because: [false dichotomy detected /
decision-type prompt / 3 sub-problems identified]. Here are your options:"

## Implementation

### Step 0: Pre-Transformation Audit

Before rewriting, run these 4 checks:

1. **Assumption scan:** What does the prompt take for granted? Flag contestable ones.
2. **Intent consistency:** Does the stated request match the implied goal?
3. **Framing neutrality:** Is the prompt loaded or does it presuppose a conclusion?
4. **Scope check:** Is this decomposable, or a single ask hiding sub-problems?

If any check fails → fix before transforming (neutralise, expand, decompose).
Consult the Fallacy Detection table for specific correction strategies.

### Step 1: Classify

Use the Prompt Classification Router to determine which expert patterns apply.
If a prompt spans multiple types (e.g., Decision + Creative), combine the
pattern sets from each applicable type.

### Step 2: Select Mode

Apply Mode Selection Logic. If interactive: state rationale, then present 2-3
framing options with trade-offs for each.

If the user declines options ("just rewrite it"), apply the broadest framing
(expanded scope, neutralised assumptions) and deliver as automatic mode.

### Step 3: Transform

Apply the patterns identified in Step 1. For Decision/Analytical prompts,
additionally embed reasoning cues:

- "Consider at least two alternatives before recommending"
- "For each option, list supporting and contradicting evidence"
- "State your confidence level and what would change your mind"
- "Check whether your recommendation holds if the key assumption is wrong"

Do not name any framework.

### Step 4: Verify

Before delivering, run 4 checks:

| Test | Pass criterion | Fail action |
|------|---------------|-------------|
| Intent preservation | Original user would say "yes, that's what I meant" | Rewrite |
| No invention | Every added element traces to a gap in the original | Remove |
| Recognition | Original user recognises their request in the rewrite | Simplify |
| Proportionality | Complexity proportional to task complexity | Scale up/down |

### Step 5: Deliver

**Automatic mode:** Single rewrite + brief "what changed" note.

**Interactive mode:** 2-3 options, each with trade-offs. User selects.
Then deliver the chosen rewrite + "what changed" note.

For full transformation examples, see `examples.md`.

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Amplifying a false dichotomy | Pre-audit catches structure before rewrite |
| Preserving loaded framing | Neutralise framing, preserve the *question* |
| Numbering instead of decomposing | Identify dependencies, priorities, deferrals |
| Skipping audit for "simple" prompts | Simple prompts hide the most errors |

### Rationalization Table

| Excuse | Reality |
|--------|---------|
| "This prompt is simple, skip the audit" | Simple prompts have the most hidden assumptions. 30 seconds saves the rewrite. |
| "Audit is overkill" | 4 questions. The alternative is an expert-sounding wrong answer. |
| "I'm preserving their intent" | Check: are you preserving their *goal* or their *wording*? |
| "Adding alternatives is inventing" | Expanding a false dichotomy isn't invention — it's correction. |

## Constraints

- **Preserve intent, not wording.** The goal is what they want, not how they said it.
- **Don't invent requirements.** Fill gaps with defaults; don't add things they didn't imply.
- **Correct terminology, not impressive.** Domain language clarifies — it doesn't intimidate.
- **Match complexity to task.** Simple question → clear rewrite. Not PhD-level complexity.
- **Surface ambiguity only when guessing wrong = significantly worse outcome.**

## Output

**Automatic mode:**
```
**Expert rewrite:** [rewritten prompt]

**What changed:** [1-2 sentence explanation]
```

**Interactive mode:**
```
Processing in interactive mode because: [rationale]

**Option A:** [framing + trade-off]
**Option B:** [framing + trade-off]
**Option C:** [framing + trade-off] (if applicable)

Which approach fits your intent?
```

After user selects:
```
**Expert rewrite:** [chosen option, fully written]

**What changed:** [explanation]
**Assumptions made:** [if any]
```
