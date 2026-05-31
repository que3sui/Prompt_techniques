# Output Quality Control / 输出质量控制

> Techniques for controlling AI output style, information density, and readability. Prevent jargon-heavy, bloated, or shallow responses.

---

## 场景描述 / Scenario

AI 模型默认倾向于生成 "看起来完整" 的输出，但这不总是你需要的。有时你需要高密度信息，有时你需要通俗解释。学会主动控制输出质量，而不是接受 "还不错" 的默认输出。

---

## 技巧 / Techniques

### 1. 信息密度控制 / Information Density Control

**问题：** AI 输出的信息密度往往偏低，长篇内容中有效信息占比不足。你以为看了很多，实际上吸收的很少。

> **AI的信息密度往往会带给你错觉，它输出的内容越长，就越需要个人来蒸馏，不然你就是长江黄河在面前奔涌而过，你却一捧水都不喝。**

**应对：** 主动要求蒸馏。让 AI 先给出摘要，再按需展开。

**Prompt 模板：**

```
请将以下内容分三层输出：
1. 三句话摘要（给只有 30 秒的人）
2. 核心要点（给有 3 分钟的人）
3. 完整展开（给需要深入了解的人）
```

**English version:**

```
Present the following in three layers:
1. Three-sentence summary (for someone with 30 seconds)
2. Key points (for someone with 3 minutes)
3. Full elaboration (for someone who needs deep understanding)
```

---

### 2. 防术语堆砌 / Anti-Jargon

**问题：** AI 习惯用专业术语来显得权威，但过度的术语堆砌反而阻碍理解。尤其是当术语没有被解释时。

**应对：** 在 prompt 中明确术语约束。

**Prompt 模板：**

```
有几点关于输出风格的硬性要求：
- 禁止专业术语的堆砌
- 涉及公式时需要解释每一个量代表的意思
- 比喻要合理且易于记忆，通俗后仍要具备专业性的讲解
```

**English version:**

```
Hard requirements on output style:
- No jargon stacking without explanation
- For any formula, explain what each variable represents
- Use memorable analogies, but ensure they maintain technical accuracy after simplification
```

---

### 3. 长度与完整性 / Length vs. Completeness

**问题：** AI 有时会因为担心输出太长而自行缩减内容。如果你的需求是完整性优先，需要明确告知。

**应对：** 直接要求 "不要因为过长而缩减内容，宁愿分为多次展开"。

**Prompt 模板：**

```
不要因为输出长度而缩减内容。如果你判断内容过长，主动告知我分多次输出，但不要自行做删减。知识的完整性和体系性优先于输出长度。
```

**English version:**

```
Do not trim content due to output length. If you judge the content is too long for one response, tell me and split into multiple outputs — but do not self-censor or condense. Completeness and systematic coverage take priority over brevity.
```

---

## 为什么有效 / Why It Works

AI 的训练目标包含 "用户满意度"，所以它会本能地给出 "看起来好" 的输出 —— 这可能意味着挺长、挺专业、挺流畅，但不一定等于你需要的输出。通过在 prompt 中明确输出质量标准，你实际上是重新定义了 "好的输出" 是什么。

Related techniques:

- [`techniques/critical-check.md`](techniques/critical-check.md) — detecting common output traps
- [`techniques/thinking-chain.md`](techniques/thinking-chain.md) — ensuring reasoning depth

---

## 注意事项 / Caveats

- 不同的任务需要不同的输出风格 —— 一个 prompt 不会适合所有场景
- 过于严格的约束可能导致 AI 过度谨慎，失去创造性
- 根据实际效果微调，而非一次性设定完就不改
