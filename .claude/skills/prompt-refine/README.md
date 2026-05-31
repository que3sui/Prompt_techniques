# Prompt Refine Skill

A Claude Code skill that optimizes your prompts using battle-tested techniques from the [Prompt_techniques](../) repository. It reads the scenarios and techniques you've collected, matches them to your intent, and outputs a refined prompt — then continues the conversation with it.

## What It Does

- Reads your prompt draft
- Auto-matches relevant techniques (role design, thinking chain, output quality, critical checks)
- Outputs an optimized, ready-to-use prompt with a summary of changes
- Automatically continues the conversation using the refined prompt

## Installation

### Global (recommended)

Copy the skill to Claude Code's global skills directory so it works in any project:

```bash
cp -r .claude/skills/prompt-refine ~/.claude/skills/prompt-refine
```

Restart Claude Code or start a new session. The skill will auto-detect when you need prompt help.

### Project-only

The skill is already in `.claude/skills/prompt-refine/`. Claude Code auto-discovers project-local skills — no extra setup needed if you're working in this repo.

## Usage

**Auto-detect:** Just type a prompt you want to use. The skill activates when it detects your prompt could benefit from improvement.

**Explicit:** Say "refine this prompt", "optimize my prompt", or type `/prompt-refine`.

**Example:**

```
User: I want to ask AI to explain machine learning to me.

Skill activates → reads repo → applies role-persona + output-quality techniques

Output:
## Refined Prompt
请你以一个逻辑严密、类比生动的教授身份，给我完整讲述机器学习的基础概念。
注意：禁止术语堆砌，每个概念用一句话解释后再深入。比喻要通俗且准确。

## Key Changes
- Applied role-persona: Added "professor" persona with specific traits
- Applied output-quality: Added anti-jargon constraints and analogy requirements
```

## How It Works

1. Reads your repo at `E:/AlphaLab/prompt_technique/` for techniques and scenarios
2. Analyzes your prompt's intent and weaknesses
3. Applies matching techniques from `techniques/`
4. Outputs refined prompt + change summary
5. Continues the conversation with the refined prompt

## Repository Structure

The skill depends on the Prompt_techniques repo structure:

```
scenarios/     → Use-case prompts (academic, investment, product, career)
techniques/    → Methods (role-persona, thinking-chain, output-quality, critical-check)
template.md    → Entry format reference
```
