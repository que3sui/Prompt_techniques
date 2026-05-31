# Prompt Techniques Repository — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create the prompt-techniques open-source repository with 12 files: 3 root docs (README, LICENSE, CONTRIBUTING), 4 scenario files, 4 technique files, and 1 template.

**Architecture:** Pure Markdown documentation repo. `scenarios/` holds reader-facing prompt collections organized by use case; `techniques/` holds cross-cutting methodology explanations. Each file follows a unified template. No build step, no dependencies.

**Tech Stack:** Markdown only. No code, no tests, no CI.

---

### Task 1: Create template.md

**Files:**

- Create: `template.md`

- [ ] **Step 1: Write template.md**

````markdown
# [Title in English] / [中文标题]

> [2-3 sentence English abstract summarizing this entry]

---

## 场景描述 / Scenario

[When and why to use this. What problem does it solve? What situation is the reader in?]

---

## Prompt 模板 / Prompt Template

[Copy-paste ready prompt with `{{placeholders}}` for user-specific parts]

```
[The actual prompt text]
```

**English version:**

```
[English translation of the prompt]
```

---

## 为什么有效 / Why It Works

[Explain the underlying mechanics. Which techniques are at play? Link to relevant files in `techniques/`.]

Related techniques:

- [`techniques/xxx.md`](techniques/xxx.md) — [one-line description]

---

## 注意事项 / Caveats

- [Edge case or known limitation]
- [When this prompt might NOT work well]
````

- [ ] **Step 2: Commit**

```bash
git add template.md
git commit -m "feat: add entry template"
```

---

### Task 2: Create techniques/critical-check.md

**Files:**

- Create: `techniques/critical-check.md`

- [ ] **Step 1: Write techniques/critical-check.md**

````markdown
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
````

- [ ] **Step 2: Commit**

```bash
git add techniques/critical-check.md
git commit -m "feat: add critical-check technique"
```

---

### Task 3: Create techniques/output-quality.md

**Files:**

- Create: `techniques/output-quality.md`

- [ ] **Step 1: Write techniques/output-quality.md**

````markdown
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
````

- [ ] **Step 2: Commit**

```bash
git add techniques/output-quality.md
git commit -m "feat: add output-quality technique"
```

---

### Task 4: Create techniques/role-persona.md

**Files:**

- Create: `techniques/role-persona.md`

- [ ] **Step 1: Write techniques/role-persona.md**

````markdown
# Role & Persona Design / 角色与人格设定

> Designing effective AI personas to shape response depth, style, and perspective. A well-designed persona produces dramatically better output than a generic "be helpful" prompt.

---

## 场景描述 / Scenario

当你给 AI 设定一个具体的角色身份时，它的输出质量会显著提升。这不是玄学 —— 角色设定实际上是在隐式地指定知识深度、语言风格、推理方式和对读者的假设。

---

## 技巧 / Techniques

### 1. 单一权威角色 / Single Authority Persona

**适用场景：** 需要系统性、完整性的知识讲解。

**设计要素：**

- 身份（教授/工程师/分析师）
- 特质（逻辑严密、理论扎实、类比生动通俗）
- 对读者的假设（刚刚读完论文、有一定基础但需要梳理）

**Prompt 模板：**

```
请你以一个逻辑严密、理论扎实、类比生动通俗的教授身份，给我完整讲述[主题]。

注意事项：
- 我看重内容的推理过程以及概念之间的逻辑演进关系
- 我欣赏知识的完整性和体系性，越详实越好
- 如果有逻辑上的缺失，记得补上并做备注
- 禁止专业术语的堆砌，涉及公式需要解释每一个量代表的意思
- 比喻要合理且易于记忆，通俗后要具备专业性的讲解
```

**English version:**

```
As a professor known for rigorous logic, solid theoretical grounding, and vivid, accessible analogies, give me a complete explanation of [topic].

Requirements:
- I value the reasoning process and the logical progression between concepts
- I appreciate thoroughness and systematic coverage — the more detailed, the better
- If there are logical gaps, fill them in and note where you did
- No jargon stacking; for any formula, explain every variable
- Use memorable, apt analogies that retain technical accuracy
```

---

### 2. 多角色辩论 / Multi-Persona Debate

**适用场景：** 需要从多个维度审视一个问题，获得对立视角。

**设计要素：**

- 两个或更多有明确立场差异的角色
- 每个角色的思维框架要明确（如 "巴菲特式价值投资" vs "索罗斯式反身性"）
- 不仅要求辩论，还要求辩论后给出综合洞察

**Prompt 模板：**

```
请你分别以[A身份]和[B身份]的视角展开辩论，讨论[问题]。

一人追求[特质A]，另一人追求[特质B]。辩论后，给出你对这个话题的综合判断。
```

**English version:**

```
Debate [question] from two perspectives: as a [Role A — describe traits] and as a [Role B — describe traits]. After the debate, provide your synthesis and judgment on the topic.
```

---

### 3. 苏格拉底式提问者 / Socratic Questioner

**适用场景：** 你需要被 "考问" 来检验自己的理解，而不是被动接收信息。

**设计要素：**

- AI 的角色是提问者，而非回答者
- 问题要有层次、有逻辑递进
- 允许纠错和多轮对话

**Prompt 模板：**

```
我是一个刚读完某个主题的人。请你做以下几件事：
1. 完整理解[材料]的内容和逻辑主线
2. 为我设计一整套由浅入深的问题，问题之间要有层次和逻辑递进
3. 你一个一个地提问，我来回答，你在对话中纠错和补充
4. 最后输出结构化的 Q&A 文档

我的偏好：看重推理过程、欣赏完整性和体系性、要求通俗与专业兼具。
```

**English version:**

```
I've just finished reading [material]. Do the following:
1. Fully understand the content and its logical thread
2. Design a comprehensive set of questions, from basic to advanced, with logical progression between them
3. Ask me one question at a time — I'll answer, and you correct and supplement in real time
4. Output a structured Q&A document at the end

Preferences: value reasoning process, appreciate systematic completeness, balance accessibility with rigor.
```

---

## 为什么有效 / Why It Works

角色设定本质上是一种 **隐式 prompt engineering**。当你指定 "一位逻辑严密、理论扎实的教授" 时，你调用了模型训练数据中与该角色相关的所有隐性知识 —— 教授如何组织内容、教授如何选择例证、教授如何评估读者的理解水平。这些隐性约束比显式指令更丰富、更自然。

Related techniques:

- [`techniques/thinking-chain.md`](techniques/thinking-chain.md) — ensuring the persona actually reasons, not just performs
- [`techniques/output-quality.md`](techniques/output-quality.md) — controlling persona's output style

---

## 注意事项 / Caveats

- 角色越具体，效果越好。避免 "你是一个专家" 这种模糊设定
- 角色设定的效果与任务匹配度有关 —— 让教授角色写代码可能不如让工程师角色
- 角色的 "个性" 可能导致偏见 —— 对于需要中立分析的任务，用辩论框架来对冲
````

- [ ] **Step 2: Commit**

```bash
git add techniques/role-persona.md
git commit -m "feat: add role-persona technique"
```

---

### Task 5: Create techniques/thinking-chain.md

**Files:**

- Create: `techniques/thinking-chain.md`

- [ ] **Step 1: Write techniques/thinking-chain.md**

````markdown
# Chain-of-Thought Guidance / 思维链引导

> Making AI show its work — step-by-step reasoning, logical progression, and gap detection. The difference between "getting an answer" and "understanding how we got there."

---

## 场景描述 / Scenario

AI 擅长直接给出结论，但结论背后的推理过程才是真正有价值的部分。通过引导 AI 展示思维链，你获得的是：可验证的推理路径、可发现的知识盲区、可复用的思考框架。

---

## 技巧 / Techniques

### 1. 推理优先级 / Reasoning Priority

**核心原则：** 让 AI 知道 "推理过程" 比 "最终答案" 更重要。如果 AI 认为你只关心结果，它会更倾向于跳过推理步骤。

**Prompt 模板：**

```
在回答中，请明确区分：
- 推理过程（你是怎么从 A 推演到 B 的）
- 中间假设（哪些步骤是基于假设而非确定事实）
- 最终结论

我优先看推理过程。如果推理过程出错，即使结论碰巧正确，也是不合格的。
```

**English version:**

```
In your response, clearly distinguish:
- Reasoning process (how you got from A to B step by step)
- Intermediate assumptions (which steps rely on assumptions vs. established facts)
- Final conclusion

I prioritize reasoning over answers. If the reasoning is flawed, correct conclusions by coincidence still don't count.
```

---

### 2. 逻辑缺失补全 / Gap Filling

**核心原则：** AI 的默认行为是 "流畅地跳过逻辑空白"，因为它被训练为输出连贯的文本而非严谨的逻辑。你需要主动要求它标注并填补空白。

**Prompt 模板：**

```
在推理过程中，如果你发现某个逻辑跳步（从 P 直接到 R 但 Q 缺失），请：
1. 明确标注 "此处存在逻辑跳跃"
2. 补充缺失的中间步骤
3. 确认补充后的链条是否完整

如果有逻辑上的缺失，补上并做备注。
```

**English version:**

```
During reasoning, if you detect a logical jump (P straight to R with Q missing):
1. Clearly mark "logical jump detected here"
2. Fill in the missing intermediate steps
3. Confirm whether the chain is now complete

If there are gaps, fill them and note where you did.
```

---

### 3. 分层推理 / Layered Reasoning

**核心原则：** 对于复杂问题，要求 AI 在不同的抽象层次上进行推理 —— 先整体框架，再细节展开。

**Prompt 模板：**

```
请按以下层次展开推理：
1. 宏观框架：大的逻辑主线是什么？（3-5 步）
2. 中观推演：每一步内部的具体推理过程
3. 微观细节：关键步骤涉及的具体计算或证据
4. 反向检验：用结论倒推前提，检查一致性
```

**English version:**

```
Layered reasoning:
1. Macro: What's the main logical thread? (3-5 high-level steps)
2. Meso: Detailed reasoning within each step
3. Micro: Specific calculations or evidence for key steps
4. Reverse test: Work backwards from conclusion to premises — check consistency
```

---

## 为什么有效 / Why It Works

AI 语言模型本质上是 "下一个 token 预测器"，它的默认行为是生成连贯的文本序列，而不是进行严谨的逻辑推理。思维链引导通过显式要求逐步推演，把模型从 "流利生成模式" 切换到 "审慎推理模式" —— 每一步的输出变成了上一步的输入条件，形成自校正循环。

Related techniques:

- [`techniques/role-persona.md`](techniques/role-persona.md) — designing personas that naturally reason more deeply
- [`techniques/critical-check.md`](techniques/critical-check.md) — verifying the reasoning chain after the fact

---

## 注意事项 / Caveats

- 即使展示了思维链，AI 仍可能 "自信地错误推理" —— 需要批判性校验
- 推理链过长时，AI 可能在中途 "迷失方向"，分层推理可以部分缓解这个问题
- 对于简单问题，过度要求推理链反而浪费时间
````

- [ ] **Step 2: Commit**

```bash
git add techniques/thinking-chain.md
git commit -m "feat: add thinking-chain technique"
```

---

### Task 6: Create scenarios/academic.md

**Files:**

- Create: `scenarios/academic.md`

- [ ] **Step 1: Write scenarios/academic.md**

````markdown
# Academic Research & Paper Study / 学术研究与论文研读

> Prompts for deep reading, systematic note-taking, and Socratic self-examination when studying papers or academic material.

---

## 场景描述 / Scenario

你正在阅读论文或学术材料，需要的不只是摘要和翻译，而是：

- 理解论文的逻辑主线和各个推导步骤
- 检验自己的理解（而非被动接收）
- 输出可保留的结构化笔记

---

## Prompt 1: 教授式深度讲解 / The Professor Deep-Dive

**适用场景：** 刚读完一篇论文或一批文件，需要系统性梳理内容。

```
请你以一个逻辑严密、理论扎实、类比生动通俗的教授身份，给我完整讲述这些文件涉及的内容。

有几点需要注意：
- 我看重内容的推理过程以及文件之间的逻辑关系
- 我欣赏知识的完整性和体系性，越详实越好
- 如果有逻辑上的缺失，记得补上并做备注
- 禁止专业术语的堆砌，涉及公式需要解释每一个量代表的意思
- 比喻要合理且易于记忆，通俗后要具备专业性的讲解
- 内容存在obsidian里（新建一个文件夹），不要因为过长而缩减内容，宁愿分为多次写入
```

**English version:**

```
As a professor known for rigorous logic, solid theory, and vivid analogies, give me a complete walkthrough of these documents.

Requirements:
- I value the reasoning process and the logical relationships between documents
- I appreciate systematic completeness — the more detailed, the better
- If there are logical gaps, fill them and note where
- No jargon stacking; explain every variable in formulas
- Use memorable, apt analogies that retain technical accuracy
- Save content to Obsidian (create a new folder). Do not condense — split across multiple outputs if needed.
```

**Why it works:** The "professor" persona frames the AI's output as a lecture — this implicitly activates structured, pedagogical thinking. The explicit instruction to "补上逻辑缺失" forces the model to audit its own reasoning. See [`techniques/role-persona.md`](../techniques/role-persona.md) and [`techniques/thinking-chain.md`](../techniques/thinking-chain.md).

---

## Prompt 2: 苏格拉底式论文研读 / Socratic Paper Examination

**适用场景：** 读完论文后准备汇报（组会、答辩），需要深度理解并预判提问。

```
回到刚刚的话题，这是一个关于[主题]的研究仓库，我已完成基本的阅读，现在打算完成汇报PPT，汇报给[受众]。

我需要你做以下几件事：
1. 完整阅读并理解论文内容，理解逻辑主线与技术方法
2. 针对我这个刚刚读完论文的人，根据论文内容，提出你认为有价值的问题（尽可能多而全面）
   - 可以是对基础概念的提问
   - 可以是对逻辑链条的提问
   - 可以是对技术细节的提问
   - 问题间要有层次和逻辑递进
3. 你把问题写进文件里，然后一个一个地提问我，我会回答问题
   - 你在对话过程中纠错和补充（允许多轮，直到概念清晰）
   - 时刻保持提问的逻辑递进
4. 最后输出结构：Problem A + Answer A; Problem B + Answer B; ...

我的偏好（请记住）：
- 我看重推理过程以及概念之间的逻辑演进关系
- 我欣赏知识的完整性和体系性，越详实越好
- 如果有逻辑上的缺失，记得补上并做备注
- 禁止专业术语的堆砌
- 涉及公式需要解释每一个量代表的意思
- 比喻要合理且易于记忆，通俗后要具备专业性的讲解
- 不要因为过长而缩减内容，宁愿分为多次展开
```

**English version:**

```
I've finished reading the research on [topic] and need to prepare a presentation for [audience].

Do the following:
1. Fully understand the paper — logic thread and technical methods
2. Based on the paper, generate comprehensive, well-structured questions for me:
   - Basic concept questions
   - Logical chain questions
   - Technical detail questions
   - Questions should have layered, progressive logic
3. Write questions to a file, then quiz me one at a time
   - Correct and supplement my answers in real time (multiple rounds until clear)
   - Maintain logical progression between questions
4. Final output: Problem A + Answer A; Problem B + Answer B; ...

Preferences:
- Value reasoning process and logical progression between concepts
- Thoroughness and systematic coverage preferred
- Fill logical gaps and note them
- No jargon stacking; explain formula variables
- Vivid, accurate analogies
- Do not condense for length — split across outputs if needed
```

**Why it works:** This flips the AI from "teacher" to "examiner," creating active learning instead of passive consumption. The structured Q&A format builds a personal knowledge base. See [`techniques/role-persona.md`](../techniques/role-persona.md).

---

## 注意事项 / Caveats

- 教授式讲解适合 "首次学习"，苏格拉底式更适合 "检验学习"
- 如果论文涉及前沿领域，AI 的知识截止日期可能导致遗漏最新进展，记得追问
- 对于数学密集型论文，要求 AI 逐行解释推导步骤，而非概括性描述
````

- [ ] **Step 2: Commit**

```bash
git add scenarios/academic.md
git commit -m "feat: add academic scenario"
```

---

### Task 7: Create scenarios/investment.md

**Files:**

- Create: `scenarios/investment.md`

- [ ] **Step 1: Write scenarios/investment.md**

````markdown
# Investment Analysis / 投资分析

> Prompts for financial data analysis, multi-perspective debate, and systematic research planning. Designed for scenarios where you have extensive data and need structured guidance on what to do with it.

---

## 场景描述 / Scenario

你手上有大量金融数据（价格、基本面、资金流向、新闻情绪等），想知道 "我能用这些数据做什么有价值的分析"。与其一个个尝试，不如先用辩论框架激发视角，再用教授式讲解系统性学习。

---

## Prompt 1: 双视角辩论 / Dual-Perspective Debate

**适用场景：** 面对丰富的数据集，不确定分析方向时，用对立视角碰撞出可能性。

```
请你分别以一个兼具学术维度的极繁高深与市场维度的极简通透的教授身份，
和一个拥有巴菲特式价值投资思维与索罗斯式反身性洞察的股神级投资专家的视角，
展开辩论。

如果我拿到了以下数据，我能展开哪些有价值的分析？

数据集：
- 过去近10年的股票数据
- 所有股票的基础信息列表
- 交易日历数据
- 按交易日存储的A股日频量价数据目录（从2016年起至今）
- 个股每日重要的基本面指标数据
- 市场指数数据
- 沪深A股每日资金流向数据
- 东方财富每日新闻快讯数据（2019年至今）
- 每日的ST股票列表
```

**English version:**

```
Debate from two perspectives:
- A professor combining academic depth (rigorous theory) with market clarity (distilled insight)
- An investment expert with Buffett-style value investing thinking and Soros-style reflexivity insight

Given the following dataset, what valuable analyses can I conduct?

Data available:
- ~10 years of stock data
- Full stock master list
- Trading calendar
- Daily A-share price/volume data (from 2016)
- Daily fundamental indicators per stock
- Market index data
- Daily capital flow data (Shanghai/Shenzhen A-shares)
- Dongfang Caixin daily news briefs (from 2019)
- Daily ST stock list
```

**Why it works:** 两个对立视角覆盖了 "学术系统性" 和 "实战直觉" 两个维度，辩论形式让 AI 互相挑战，产出比单一视角更全面的分析路线图。See [`techniques/role-persona.md`](../techniques/role-persona.md).

---

## Prompt 2: 分析内容的系统性讲解 / Systematic Analysis Deep-Dive

**适用场景：** 辩论结束后，有了分析方向的清单，需要深入了解每个方向的具体方法论。

```
给我完整讲述这些分析涉及的专业内容。

有几点需要注意：
- 我看重内容的推理过程以及概念之间的逻辑演进关系
- 我欣赏知识的完整性和体系性，越详实越好
- 如果有逻辑上的缺失，记得补上并做备注
- 禁止专业术语的堆砌
- 涉及公式需要解释每一个量代表的意思
- 要善用比喻，且比喻要合理且易于记忆，通俗后要具备专业性的讲解
- 不要因为过长而缩减内容，宁愿分为多次展开
```

**English version:**

```
Give me a complete explanation of the professional content behind these analyses.

Requirements:
- I value reasoning process and logical progression between concepts
- Thoroughness and systematic coverage — the more detailed, the better
- Fill logical gaps and note them
- No jargon stacking
- Explain every variable in formulas
- Use memorable, apt analogies that retain technical accuracy
- Do not condense for length — split across multiple outputs if needed
```

**Why it works:** 这个 prompt 把 "完整性" 和 "可理解性" 设为硬约束，防止 AI 给出蜻蜓点水式的概述。See [`techniques/output-quality.md`](../techniques/output-quality.md) and [`techniques/thinking-chain.md`](../techniques/thinking-chain.md).

---

## 注意事项 / Caveats

- 投资分析有重大风险：AI 的分析仅供参考，不构成投资建议
- 金融数据通常需要预处理（缺失值、复权、幸存者偏差），这些在 prompt 中没有覆盖，需要额外确认
- 辩论框架产生的分析方向可能过多 —— 建议先选出 2-3 个最有价值的深入
````

- [ ] **Step 2: Commit**

```bash
git add scenarios/investment.md
git commit -m "feat: add investment scenario"
```

---

### Task 8: Create scenarios/product.md

**Files:**

- Create: `scenarios/product.md`

- [ ] **Step 1: Write scenarios/product.md**

````markdown
# Product Validation / 产品验证

> Prompts for stress-testing product ideas with constraint-based reasoning, red-team mechanisms, and strategic pipeline analysis — tailored for small-team developers.

---

## 场景描述 / Scenario

你有一个产品想法，资源有限（小团队），需要在动手之前尽可能全面地检验它的可行性。AI 可以帮助模拟约束推演、红队攻击和战略分析。

---

## Prompt: 产品验证工作坊 / Product Validation Workshop

**适用场景：** 产品早期的概念验证，用几个核心机制快速检验想法是否站得住脚。

```
验证一个产品，尝试以下几个机制：

1. 明确任务边界
   - 这个产品具体要解决什么问题？
   - 不解决什么问题？（约束范围）
   - 用户是谁？不是谁？

2. 带约束的推演（限于小团队开发者）
   - 假设只有 2-3 人的开发团队
   - 3 个月内必须上线 MVP
   - 在此约束下，哪些功能必须砍掉？哪些是核心？

3. 引入冲突与红队机制
   - 请模拟一个对该产品最悲观的批评者
   - 这个产品最可能因为什么失败？
   - 给出三个最致命的 "如果不解决就会死" 的问题

4. 分析流水线（战略工作坊输出）
   - 用户获取 → 激活 → 留存 → 收入 → 传播
   - 每一环节的具体策略是什么？
   - 哪个环节最薄弱？

最后给出综合判断：这个产品在当前约束下是否值得做？
```

**English version:**

```
Validate a product idea using these mechanisms:

1. Define task boundaries
   - What specific problem does this solve?
   - What does it NOT solve? (scope constraint)
   - Who is the user? Who is NOT the user?

2. Constraint-based reasoning (small team)
   - Assume a 2-3 person dev team
   - MVP must ship within 3 months
   - Under these constraints, what MUST be cut? What's truly core?

3. Red-team / adversarial review
   - Simulate the most pessimistic critic of this product
   - What's the most likely reason this fails?
   - Name three "will die if not solved" problems

4. Pipeline analysis (strategy workshop output)
   - Acquisition → Activation → Retention → Revenue → Referral
   - What's the specific strategy for each stage?
   - Which stage is weakest?

Final judgment: given these constraints, is this product worth building?
```

**Why it works:** 这套机制将模糊的 "这个想法行不行" 拆解为四个具体维度，每个维度有明确的评判标准。红队机制特别关键 —— 它强制 AI 站在对立面思考，对抗确认偏误。See [`techniques/thinking-chain.md`](../techniques/thinking-chain.md) and [`techniques/critical-check.md`](../techniques/critical-check.md).

---

## 注意事项 / Caveats

- AI 的红队批评基于训练数据中的模式，不能替代真实用户反馈
- 约束推演的结果取决于约束设定的合理性 —— 如果实际约束与假设差异大，结论会偏
- 这个框架更适合做 "初始过滤"（排除明显不可行的想法），而非 "最终决策"
````

- [ ] **Step 2: Commit**

```bash
git add scenarios/product.md
git commit -m "feat: add product scenario"
```

---

### Task 9: Create scenarios/career.md

**Files:**

- Create: `scenarios/career.md`

- [ ] **Step 1: Write scenarios/career.md**

````markdown
# Career Thinking in the AI Era / AI时代的职业思考

> Prompts for reflecting on what work is truly valuable when AI tools like Claude can write code, analyze data, and generate content at scale.

---

## 场景描述 / Scenario

当你发现 AI 可以写代码、做分析、写报告时，自然会问：我的价值在哪里？什么样的项目和工作在 AI 时代更有意义？这些 prompt 帮助你进行结构化反思。

---

## Prompt: 重新定义有价值的工作 / Redefining Valuable Work

**适用场景：** 感到 AI 正在替代大量传统工作内容时，重新思考方向。

```
你要知道，在这个时代里，古法编程也就是手搓代码，已经被大多数人淘汰了。
以往对于项目时间的评估可能通过类似Claude的实现就搞定了，
同样以往对于一些复现的工作价值已经大不如前了（或者你来反驳我）。

在这样的情况下，你来告诉我：
1. 真正有价值、适合Claude开发的项目是什么？
2. 什么样的工作AI无法替代？
3. 开发者应该如何调整自己的技能组合？
```

**English version:**

```
Acknowledge this reality: traditional hand-coded programming is being phased out for most people.
Project time estimates can now be done by tools like Claude.
The value of reproduction/implementation work has declined sharply (feel free to push back on this).

Given this, tell me:
1. What kind of projects are truly valuable and well-suited for AI-assisted development?
2. What work can AI NOT replace?
3. How should developers adjust their skill portfolio?
```

**Why it works:** 这个 prompt 的关键在于 "或者你来反驳我" —— 它防止 AI 只是附和你的前提，而是要求批判性思考。综合判断比单向论证更有价值。See [`techniques/critical-check.md`](../techniques/critical-check.md).

---

## 注意事项 / Caveats

- AI 对 "什么有价值" 的判断基于训练数据中的观点分布，不是真理
- 这类问题的价值更多在于激发思考，而非获得 "标准答案"
- 建议把 AI 的输出作为讨论起点，和真实的人（同行、导师）进一步探讨
````

- [ ] **Step 2: Commit**

```bash
git add scenarios/career.md
git commit -m "feat: add career scenario"
```

---

### Task 10: Create CONTRIBUTING.md

**Files:**

- Create: `CONTRIBUTING.md`

- [ ] **Step 1: Write CONTRIBUTING.md**

```markdown
# Contributing to Prompt Techniques

Thanks for your interest in contributing! This is a community-driven handbook of battle-tested prompt patterns. Contributions of all kinds are welcome — new prompts, translations, improvements to explanations, or bug fixes.

## How to Contribute

### 1. Pick Something to Work On

- **Add a new scenario:** Found a use case not yet covered? Write it up.
- **Add a new technique:** Discovered a reusable prompt pattern? Share it.
- **Improve an existing entry:** Better explanation, clearer template, new caveat? Go for it.
- **Translation:** Help translate existing entries into your language.

### 2. Use the Template

All entries follow [`template.md`](template.md). Please use it as your starting point:

1. Copy `template.md` to the right directory (`scenarios/` or `techniques/`)
2. Fill in every section
3. Link to related techniques or scenarios where relevant

### 3. Style Guidelines

- **Bilingual:** Every entry should have English headers and an English abstract. Prompt content should include both the original language and an English translation.
- **Show, don't just tell:** Every technique must include at least one copy-paste-ready prompt.
- **Explain why:** Don't just show the prompt — explain why it works.
- **Be honest about limitations:** Every entry should have caveats. No technique works everywhere.

### 4. Submit a Pull Request

1. Fork the repo
2. Create a feature branch: `git checkout -b add-xxx-scenario`
3. Commit your changes
4. Push and open a PR against `main`

### 5. PR Review Process

- PRs need one approving review
- Reviews check: does it follow the template? Is the prompt tested? Are caveats honest?
- If you've actually used the prompt in practice, mention that in the PR description — it carries weight

## What We're Looking For

- **Battle-tested:** Prompts you've actually used and refined, not hypothetical ideas
- **Generalizable:** Patterns that work across different models and contexts
- **Explained:** The "why it works" is as important as the prompt itself

## Code of Conduct

Be respectful. Assume good faith. We're here to build something useful together.
```

- [ ] **Step 2: Commit**

```bash
git add CONTRIBUTING.md
git commit -m "feat: add contribution guide"
```

---

### Task 11: Create README.md and LICENSE

**Files:**

- Create: `README.md`
- Create: `LICENSE`

- [ ] **Step 1: Write README.md**

````markdown
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

### 📖 By Scenario (I want to do X)

| I want to...                                  | Go to                                                |
| --------------------------------------------- | ---------------------------------------------------- |
| Deep-read a paper, prepare for a presentation | [`scenarios/academic.md`](scenarios/academic.md)     |
| Analyze financial data, plan research         | [`scenarios/investment.md`](scenarios/investment.md) |
| Validate a product idea before building       | [`scenarios/product.md`](scenarios/product.md)       |
| Rethink my career in the AI era               | [`scenarios/career.md`](scenarios/career.md)         |

### 🔧 By Technique (I want to learn Y)

| I want to...                     | Go to                                                          |
| -------------------------------- | -------------------------------------------------------------- |
| Design effective AI personas     | [`techniques/role-persona.md`](techniques/role-persona.md)     |
| Force step-by-step reasoning     | [`techniques/thinking-chain.md`](techniques/thinking-chain.md) |
| Control output quality & density | [`techniques/output-quality.md`](techniques/output-quality.md) |
| Detect AI output traps           | [`techniques/critical-check.md`](techniques/critical-check.md) |

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

## Contributing

See [`CONTRIBUTING.md`](CONTRIBUTING.md). New entries follow [`template.md`](template.md).

---

## License

MIT — use it, remix it, share it.
````

- [ ] **Step 2: Write LICENSE**

```
MIT License

Copyright (c) 2025

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

- [ ] **Step 3: Commit**

```bash
git add README.md LICENSE
git commit -m "feat: add README and MIT license"
```

---

### Task 12: Git init and final commit

**Files:**

- All existing files

- [ ] **Step 1: Initialize git repository**

```bash
cd E:/AlphaLab/prompt_technique
git init
```

- [ ] **Step 2: Stage all files and commit**

```bash
git add .
git commit -m "feat: initial project structure — prompt techniques handbook

Scenarios: academic, investment, product, career
Techniques: role-persona, thinking-chain, output-quality, critical-check

Co-Authored-By: Claude Opus 4.7 <noreply@anthropic.com>"
```

- [ ] **Step 3: Verify**

```bash
git status
git log --oneline
```

```

---

## Self-Review

1. **Spec coverage:** All files from the design spec are covered — README, LICENSE, CONTRIBUTING, 4 scenarios, 4 techniques, template. Content format (abstract → scenario → prompt → why → caveats) is followed in every entry.
2. **Placeholder scan:** No TBD, TODO, or vague placeholders. All code blocks contain complete content.
3. **Type consistency:** File paths, links between technique files, and section headers are consistent throughout. `template.md` defines the format and all entries follow it.

No gaps found.
```
