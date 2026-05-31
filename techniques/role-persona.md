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
