# Prompt Refine Skill

A Claude Code skill that optimizes your prompts before they reach the AI. It reads battle-tested techniques from the [Prompt_techniques](https://github.com/que3sui/Prompt_techniques) repository **and** your local memory (user preferences, project context, past feedback), matches them to your intent, then outputs a refined prompt and immediately responds to it — one continuous flow.

## What It Does

```
Your prompt → Read local memory (preferences) → Read repo (techniques)
  → Refined prompt → Immediate response (no pause)
```

1. **Reads local memory** — your preferences, project context, feedback history
2. **Reads the repo** — scenarios/ and techniques/ for matching methods
3. **Outputs refined prompt** — compact reference block
4. **Responds immediately** — continuous flow, no "want me to proceed?"

## Installation

### Global (recommended)

```bash
cp -r .claude/skills/prompt-refine ~/.claude/skills/prompt-refine
```

Works in any project. Restart Claude Code or start a new session.

### Project-only

Already in `.claude/skills/prompt-refine/`. Auto-discovered when working in this repo.

## Triggers

The skill activates when:

- You explicitly ask: "refine this", "optimize my prompt", "improve this prompt"
- You type a draft prompt that's vague, missing persona, or lacks reasoning structure
- You seem uncertain about a prompt's quality

## Usage Examples

### Example 1: Vague prompt gets refined

```
You: 教我使用Claude

Skill activates → reads memory (knows you use Claude Code, not Claude.ai)
→ reads role-persona + output-quality techniques
→ refines to a structured prompt with persona and layered output
→ responds immediately
```

### Example 2: Already good prompt, no change

```
You: 帮我在 auth.ts:42 修一下这个 JWT 过期判断的 bug

Skill: prompt is specific and actionable → skip refinement → respond directly
```

### Example 3: See what changed

```
You: 刚才改了什么？

Skill: reveals the refinement and which techniques were applied
```

## Customization

### Adding new techniques

The skill reads from `E:/AlphaLab/prompt_technique/`. When you add new scenarios or techniques to the repo, the skill automatically uses them — no skill update needed.

### Personalizing via memory

The skill checks local memory at `~/.claude/projects/E--AlphaLab-prompt-technique/memory/`. To influence its behavior:

- Feedback like "I prefer concise output" → skill stops expanding short prompts into long ones
- Project context like "this is a data analysis project" → skill biases toward matching investment/analysis scenarios
- Corrections like "don't add persona if I'm asking a quick question" → skill learns to skip refinement for short factual queries

## Files

```
prompt-refine/
├── SKILL.md    # Skill definition (loaded by Claude Code)
└── README.md   # This file (installation + usage)
```

## Troubleshooting

**Skill not triggering?** Try saying "refine this prompt" explicitly first. Auto-detection improves as you use it.

**Refinement is too aggressive?** Tell Claude "skip refinement for short questions" — this gets remembered via local memory.

**Repo path wrong?** Edit `SKILL.md` and update the `Repository` section to point to your local Prompt_techniques path.
