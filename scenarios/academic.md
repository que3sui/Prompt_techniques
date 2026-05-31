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
