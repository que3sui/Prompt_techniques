# Prompt Techniques / AI Prompt 技巧手册

> A lightweight, scenario-driven handbook of battle-tested prompt patterns.
> Make AI work for you — not the other way around.

---

## What Is This?

This is a collection of **prompt techniques that actually work** — refined through real use, not theoretical speculation. Each entry tells you:

1. **When to use it** — the scenario
2. **What to say** — the prompt, copy-paste ready
3. **Why it works** — the underlying mechanics
4. **When it doesn't** — honest caveats

---

## Quick Navigation

### By Scenario (I want to do X)

| I want to...                                  | Go to                                                |
| --------------------------------------------- | ---------------------------------------------------- |
| Deep-read a paper, prepare for a presentation | [`scenarios/academic.md`](scenarios/academic.md)     |
| Analyze financial data, plan research         | [`scenarios/investment.md`](scenarios/investment.md) |
| Validate a product idea before building       | [`scenarios/product.md`](scenarios/product.md)       |
| Rethink my career in the AI era               | [`scenarios/career.md`](scenarios/career.md)         |
| Write, review, and debug code with AI         | [`scenarios/coding.md`](scenarios/coding.md)         |

### By Technique (I want to learn Y)

| I want to...                       | Go to                                                                |
| ---------------------------------- | -------------------------------------------------------------------- |
| Design effective AI personas       | [`techniques/role-persona.md`](techniques/role-persona.md)           |
| Force step-by-step reasoning       | [`techniques/thinking-chain.md`](techniques/thinking-chain.md)       |
| Control output quality & density   | [`techniques/output-quality.md`](techniques/output-quality.md)       |
| Detect AI output traps             | [`techniques/critical-check.md`](techniques/critical-check.md)       |
| Use examples to anchor output      | [`techniques/few-shot.md`](techniques/few-shot.md)                   |
| Get structured JSON/table/template | [`techniques/structured-output.md`](techniques/structured-output.md) |

---

## Structure

```
├── scenarios/         # Reader entry point — organized by use case
├── techniques/        # Cross-cutting methods — the "why" layer
├── template.md        # Use this to add new entries
├── CONTRIBUTING.md    # How to contribute
└── LICENSE            # MIT
```

---

## Philosophy

- **Scenarios over categories.** People don't search for "role-based prompting," they search for "how to read a paper with AI."
- **Battle-tested over theoretical.** Every prompt here has been used in practice. We include the failures, not just the wins.
- **Bilingual by design.** AI prompting works across languages. This handbook should too.

---

## Claude Code Skill

This repo includes a **prompt-refine** skill for Claude Code. It auto-detects when your prompt needs improvement, matches it against techniques in this repo, and outputs a refined version — then continues the conversation with it.

```bash
# Install globally (recommended)
cp -r .claude/skills/prompt-refine ~/.claude/skills/prompt-refine
```

Then just type your prompt. The skill activates when it detects room for improvement, or say "refine this prompt" anytime. See [`.claude/skills/prompt-refine/README.md`](.claude/skills/prompt-refine/README.md) for details.

---

## Contributing

See [`CONTRIBUTING.md`](CONTRIBUTING.md). New entries follow [`template.md`](template.md).

---

## License

MIT — use it, remix it, share it.
