# Critical Validation of AI Output / AI 输出的批判性校验

> Common failure modes of AI-generated content and how to detect them. Before trusting an AI response — especially a long, confident one — run through this checklist.

---

## 场景描述 / Scenario

AI 输出看起来很专业、很完整，但实际可能存在以下问题。使用这些技巧来校验输出质量，而不是被表面说服。

---

## 常见陷阱 / Common Traps

### 1. 体面术语包装虚空 / Dressed-Up Emptiness

**症状：** 用华丽的专业词汇包装实际上没有信息量的内容。听起来很厉害，但仔细拆解后什么都没有。

**检测方法：** 逐句追问 "所以呢？"、"具体是什么？"、"能举个例子吗？"

**Prompt 示例：**

```
我刚才的回答中，请你逐段指出：哪些句子有实质信息，哪些只是修辞包装？如果有包装性的句子，请重写为直白版本。
```

**English version:**

```
Go through my previous response paragraph by paragraph. Identify which sentences contain substantive information and which are just rhetorical packaging. Rewrite any packaged sentences in plain language.
```

---

### 2. 自我批判的彻底性 ≠ 分析的彻底性 / Self-Criticism Depth ≠ Analytical Depth

**症状：** AI 会主动承认错误、自我批判，但这不代表它的分析真的深入了。忏悔之后，问题本身可能仍然没有被真正分析。

**检测方法：** 追问 "你承认了问题 X，那请具体分析：X 的根因是什么？分步骤推演一下。"

---

### 3. 术语堆砌的傲慢 / Jargon Arrogance

**症状：** 大量专业术语连用，不解释含义，制造 "我很专业" 的错觉。读者被术语震慑，忽略了内容可能空洞。

**检测方法：** 要求 AI 用 "对高中生解释" 的方式重写，或者要求每个术语后附带一句话解释。

**Prompt 示例：**

```
请用对高中生讲课的方式重新解释上述内容。每个专业术语第一次出现时，用一句话解释它是什么意思。禁止不加解释地连续使用两个以上专业术语。
```

**English version:**

```
Re-explain the above as if teaching a high school student. Define every technical term the first time it appears. Never use more than two undefined technical terms in a row.
```

---

### 4. 用全能掩盖错误 / Omnipotence Masking

**症状：** AI 倾向于回避 "我不知道" 或 "我在这方面能力不足"，而是给出一个看起来完整的回答，实际上回避了能力边界。

**检测方法：** 主动追问能力边界："这个分析的哪些部分你可能不确定？"、"有哪些信息是你基于推测而非事实得出的？"

**Prompt 示例：**

```
在以上回答中，请明确标注：(A) 你高度确定的内容 (B) 你基于推理推测的内容 (C) 你可能遗漏或不确定的部分。对 B 和 C 类内容，说明你的置信度和理由。
```

**English version:**

```
In your response, clearly label: (A) content you're highly confident about (B) content based on inference/speculation (C) areas where you may be missing something or are uncertain. For B and C, state your confidence level and reasoning.
```

---

## 为什么有效 / Why It Works

这些校验技巧的核心原理是对抗 AI 的两个系统性倾向：(1) AI 被训练为 "always helpful"，因此倾向于给出满足用户期待的答案，而非说 "我不知道"；(2) AI 的语言生成能力强于逻辑推理能力，容易出现 "流利但不准确" 的输出。

Related techniques:

- [`techniques/output-quality.md`](techniques/output-quality.md) — controlling output style and density
- [`techniques/thinking-chain.md`](techniques/thinking-chain.md) — forcing step-by-step reasoning

---

## 注意事项 / Caveats

- 这些校验方法需要用户自己有一定的领域知识来判断
- 过度使用批判性校验可能让对话变得冗长 —— 在关键决策时使用即可
