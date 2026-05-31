# Prompt Techniques Repository — Design Spec

## Goal

Open a lightweight, scenario-driven prompt technique handbook on GitHub. Bilingual (ZH + EN), structured for easy navigation by readers and simple contribution by the community.

## Target Audience

Anyone who uses AI tools (Claude, ChatGPT, etc.) and wants reusable, battle-tested prompt patterns organized by real-world scenarios.

## File Structure

```
prompt-techniques/
├── README.md                     # Bilingual intro + quick nav
├── LICENSE                       # MIT
├── CONTRIBUTING.md               # Contribution guide (ZH + EN)
│
├── scenarios/                    # 📖 Organized by use case (reader entry point)
│   ├── academic.md               #   Academic research: deep explanation, paper study
│   ├── investment.md             #   Investment analysis: data-driven A-share research
│   ├── product.md                #   Product validation: constraint reasoning, red-team
│   └── career.md                 #   Career thinking: developer value in AI era
│
├── techniques/                   # 🔧 Cross-cutting methods (the "why" layer)
│   ├── role-persona.md           #   Role design: professor, expert, debater
│   ├── thinking-chain.md         #   Chain-of-thought: reasoning over conclusions
│   ├── output-quality.md         #   Output control: anti-jargon, anti-fluff
│   └── critical-check.md         #   Critical validation: common AI output traps
│
└── template.md                   # Unified entry template for new contributions
```

## Content Format Per Entry

Each scenario and technique file follows a consistent structure:

1. **English abstract** (2-3 sentences at the top)
2. **场景描述 / Scenario** — when and why to use this
3. **Prompt 模板 / Prompt Template** — copy-paste ready, with `{{placeholders}}`
4. **为什么有效 / Why It Works** — links to relevant technique files
5. **注意事项 / Caveats** — edge cases, known limitations

## Language Strategy

- File headers and structural elements: bilingual
- Prompt content: original Chinese + English translation
- Explanations: primarily Chinese with English key points

## Non-Goals (for now)

- No static site generator, no website — plain Markdown on GitHub
- No automated testing or CI
- No categorization beyond the current 4 scenarios + 4 techniques
- No translations beyond ZH/EN (community can add later)

## Future Expansion

New scenarios or techniques follow `template.md`. Directory grows flat — no nesting beyond `scenarios/` and `techniques/`.
