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
