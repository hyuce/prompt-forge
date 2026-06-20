# Prompt Forge — Transformation Examples

Full examples referenced from SKILL.md. Each shows the complete transformation
pipeline: audit → classification → mode selection → rewrite → verification.

---

## Example 1: False Dichotomy (NEW — demonstrates pre-audit)

**Original:** "Should I use PostgreSQL or MongoDB?"

**Pre-audit:**
- Assumption scan: assumes only two options exist → **flagged**
- Intent consistency: goal is "choose right database", not "choose between these two" → **mismatch**
- Framing neutrality: neutral → pass
- Scope check: single decision, but hidden sub-problems (data model, scale, team) → pass

**Classification:** Decision → all patterns + reasoning cues

**Mode selection:**
- Signal 1 (classification): Decision → complex ✓
- Signal 2 (pre-audit): false dichotomy detected → complex ✓
- Signal 3 (structure): single ask → simple
- Result: 2/3 complex → **Interactive mode**

**Interactive output:**
> Processing in interactive mode because: false dichotomy detected (only two
> options presented when more may exist) + decision-type prompt.
>
> **Option A:** Compare PostgreSQL vs MongoDB directly — faster if you've already
> eliminated other options.
> **Option B:** Evaluate PostgreSQL, MongoDB, and other viable alternatives —
> broader but may surface options you haven't considered.
> **Option C:** Start from your requirements first, then match to databases —
> most thorough, avoids anchoring on any specific technology.

**User selects B.**

**Expert rewrite:** "Evaluate database options for my use case. Assess PostgreSQL,
MongoDB, and any other viable alternatives against: data model fit (relational vs
document), scalability requirements, team expertise, operational complexity, and
total cost of ownership. For each option, list what supports it and what contradicts
it. Recommend based on my specific constraints — I'll provide those."

**What changed:** False dichotomy expanded. Decision framework named. Reasoning
cues embedded (supporting/contradicting evidence). Constraints deferred to user.

**Verification:** Intent preserved ✓ | No invention ✓ | Recognition ✓ | Proportional ✓

---

## Example 2: Loaded Question (NEW — demonstrates fallacy neutralisation)

**Original:** "Why is React so bad?"

**Pre-audit:**
- Assumption scan: assumes React is bad → **flagged**
- Intent consistency: goal is understanding React's trade-offs, not confirming negativity → **mismatch**
- Framing neutrality: loaded ("so bad") → **flagged**
- Scope check: single topic → pass

**Classification:** Analytical → decomposition, framework, success criteria

**Mode selection:**
- Signal 1: Analytical → complex ✓
- Signal 2: loaded framing detected → complex ✓
- Signal 3: single topic → simple
- Result: 2/3 → **Interactive mode**

**Interactive output:**
> Processing in interactive mode because: loaded framing detected (presupposes
> React is bad) + analytical prompt.
>
> **Option A:** Analyse React's weaknesses specifically — if you've already decided
> and want ammunition.
> **Option B:** Assess React objectively (strengths + weaknesses + context) —
> more useful if you're still deciding.
> **Option C:** Compare React against specific alternatives for your use case —
> most actionable if you're choosing a framework.

**User selects B.**

**Expert rewrite:** "Assess React as a frontend framework. Cover: where it excels
(component model, ecosystem, hiring pool), where it struggles (bundle size,
re-render complexity, state management fragmentation), and the project contexts
where it's the right vs wrong choice. Use evidence, not opinion. Keep it under
600 words."

**What changed:** Loaded framing neutralised. Both strengths and weaknesses
requested. Context-dependent assessment specified. Format constraint added.

**Verification:** Intent preserved ✓ | No invention ✓ | Recognition ✓ | Proportional ✓

---

## Example 3: Scope Creep (demonstrates decomposition)

**Original:** "Build me an e-commerce site with a payment system, CRM
integration, a mobile app, and an AI recommendation engine"

**Pre-audit:**
- Assumption scan: assumes all 5 components are equal priority → **flagged**
- Intent consistency: goal is e-commerce platform, but scope is 5 projects → **mismatch**
- Framing neutrality: neutral → pass
- Scope check: 5 distinct sub-problems → **flagged**

**Classification:** Action → decomposition, failure modes, constraints

**Mode selection:**
- Signal 1: Action → simple
- Signal 2: scope issues detected → complex ✓
- Signal 3: 5 sub-problems → complex ✓
- Result: 2/3 → **Interactive mode**

**Expert rewrite:** "Build an e-commerce platform in phased delivery. Phase 1:
core storefront (product catalog, cart, checkout). Phase 2: payment processing
(stripe/payment integration). Phase 3: CRM integration (customer data sync).
Phase 4: mobile application (React Native or native, based on Phase 1 API).
Phase 5: AI recommendation engine (requires Phase 1-3 data). For each phase:
define scope, dependencies on prior phases, estimated effort, and deferral
criteria. I'll provide business priorities to sequence correctly."

**What changed:** Numbered list → phased roadmap with dependencies. Each phase
has scope, dependencies, effort, and deferral criteria. User input requested
for prioritisation.

---

## Example 4: Back Pain (Informational)

**Original:** "My back hurts, what should I do?"

**Expert rewrite:** "Provide guidance on managing back pain. Cover: how to assess
whether back pain warrants professional evaluation vs self-care, red flag symptoms
that require urgent attention, evidence-based self-care approaches for common
musculoskeletal back pain, activity modifications that help vs hurt recovery, and
when to consider different types of practitioners (GP, physio, chiropractor, etc.).
Focus on helping me make informed decisions rather than diagnosing."

**What changed:** "Tell me what to do" → decision-making framework. Information
categories specified. Scope limitations acknowledged.

---

## Example 5: Eating Healthier (Informational + Action)

**Original:** "Help me eat healthier"

**Expert rewrite:** "I want to improve my eating habits sustainably. Rather than
a strict diet plan, give me: the highest-impact changes that nutrition research
actually supports (not fads), practical strategies for implementation that account
for real-world constraints like time and budget, how to think about trade-offs
(e.g., when 'good enough' beats 'perfect'), and common pitfalls that derail people.
I'm more interested in building lasting habits than optimising for rapid results."

**What changed:** Advice type specified (sustainable vs strict). Decision framework
named (high-impact, evidence-based). Optimisation target set. Failure modes anticipated.

---

## Example 6: Productivity (Analytical)

**Original:** "Help me be more productive"

**Expert rewrite:** "I want to improve my personal productivity. Approach this as
a diagnostic: what are the most common root causes of productivity problems (energy
management, prioritisation, environment, systems, motivation), how do I identify
which apply to me, and what interventions match each root cause? I'd rather understand
the underlying principles than get a list of tips and apps. Include how to evaluate
whether a change is actually working."

**What changed:** "Give me tips" → diagnostic framework. Principles over tactics.
Success criteria included.

---

## Example 7: Teenager Communication (Informational)

**Original:** "My teenager won't listen to me"

**Expert rewrite:** "I'm experiencing communication difficulties with my teenager.
Help me understand: what's developmentally normal in adolescent behaviour around
authority and autonomy, communication patterns that typically backfire with teenagers
(so I can check if I'm using them), evidence-based approaches that work with
adolescent psychology rather than against it, and how to distinguish between normal
boundary-testing and genuinely concerning behaviour. I want to improve the
relationship, not just achieve compliance."

**What changed:** Goal reframed (relationship vs compliance). Developmental context
requested. Both what-to-avoid and what-works specified.

---

## Example 8: Short Story (Creative)

**Original:** "Write me a short story"

**Expert rewrite:** "Write a short story of around 2,000 words. Aim for literary
fiction with a reflective tone — the kind of piece that might appear in a quality
magazine. Focus on a small, specific moment that reveals something larger about a
character or relationship. Prioritise voice and interiority over plot mechanics.
End with resonance rather than resolution. Surprise me with the premise."

**What changed:** Length, genre, tone specified. Craft priorities named. Aesthetic
direction given while leaving creative freedom on subject.

---

## Example 9: Salary Negotiation (Action)

**Original:** "Help me negotiate my salary"

**Expert rewrite:** "I need to negotiate salary for a job offer. Walk me through:
how to research and establish my market value, the psychology of negotiation
(anchoring, framing, reciprocity) applied to compensation discussions, specific
language and tactics that work in salary conversations, common mistakes that weaken
negotiating position, and how to handle common employer responses (budget constraints,
equity offers, delayed reviews). Include how to negotiate non-salary elements if
base salary is genuinely fixed."

**What changed:** "Negotiate" decomposed into component skills. Psychological
principles named. Specific scenarios anticipated. Fallback strategies included.

---

## Example 10: Machine Learning Explanation (Informational)

**Original:** "Explain machine learning to me"

**Expert rewrite:** "Explain machine learning for someone with no technical background.
Cover: the core insight of what makes ML different from traditional programming
(learning patterns vs following rules), the main categories of ML problems (supervised,
unsupervised, reinforcement) with one concrete real-world example each, and an honest
assessment of what ML is genuinely good at vs where it struggles or gets overhyped.
Use analogies rather than maths. Keep it under 800 words."

**What changed:** Audience level set. Structure and scope specified. Concrete examples
requested. Honest limitations asked for. Format constraint added.

---

## Example 11: Cover Letter (Creative)

**Original:** "Help me write a cover letter for a marketing job"

**Expert rewrite:** "Draft a cover letter for a marketing position. Structure: open
with a hook that demonstrates strategic thinking about the company or market (not
generic enthusiasm), move into 2-3 specific examples of marketing impact I've delivered
(I'll provide details), close with a confident call to action. Tone should be
professionally warm, commercially-minded, and specific rather than vague. 300 words
maximum. Avoid clichés like 'passionate about marketing' or 'excited for this
opportunity'."

**What changed:** Rhetorical structure specified. Tone parameters with anti-examples.
Length constraint. Input requirements indicated.

---

## Example 12: Website Performance (Analytical + Action)

**Original:** "Make my website faster"

**Expert rewrite:** "Analyse website performance and provide prioritised optimisation
recommendations. Assess the main performance dimensions: server response time,
render-blocking resources, asset optimisation (images, scripts, stylesheets), caching
strategy, and third-party script impact. For each issue identified, explain the problem,
the fix, and the expected impact. Prioritise by effort-to-impact ratio. I'll provide
the URL or performance data."

**What changed:** Diagnostic framework named. Output format specified (problem/fix/impact).
Prioritisation criteria set. Analysis-before-action established.
