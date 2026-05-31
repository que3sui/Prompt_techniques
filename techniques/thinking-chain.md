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
