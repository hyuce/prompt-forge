# prompt-forge

Transform novice prompts into expert-framed requests with logical rigor.

## What This Is

An AI agent skill that bridges the gap between how non-specialists phrase requests and how domain experts would frame the same request. Unlike simple prompt rewriters, prompt-forge adds:

- **Pre-transformation audit** — catches flawed assumptions, loaded questions, and false dichotomies *before* rewriting
- **Prompt classification router** — applies the right expert patterns based on prompt type (informational, creative, analytical, action, decision)
- **Hybrid mode selection** — automatically chooses between single-rewrite (simple prompts) and interactive (complex prompts with ambiguity)
- **Post-transformation verification** — validates intent preservation, no invention, recognition, and proportionality
- **Reasoning integration** — embeds structured reasoning cues into decision/analysis prompts

## How It Differs from prompt-enhancer

| Feature | prompt-enhancer | prompt-forge |
|---------|----------------|--------------|
| Mode | Always automatic | Hybrid (auto + interactive) |
| Logical audit | None | Pre-transformation checklist |
| Fallacy detection | None | 6 common prompt fallacies |
| Classification | None | 5-type router |
| Verification | None | 4-test post-check |
| Reasoning cues | None | Conditional (decision prompts) |
| Token footprint | ~169 lines | ~158 lines (more features, less text) |

## Usage

Invoke when:
- User asks to improve, refine, or rewrite a prompt
- User needs help framing a request for an AI system
- A prompt feels vague, overloaded, or logically unsound

## Structure

```
prompt-forge/
├── SKILL.md        # Core skill logic (~158 lines)
├── examples.md     # 10 transformation examples (cross-reference)
├── README.md       # This file
└── LICENSE         # MIT
```

## License

MIT — see [LICENSE](LICENSE).
