# Coding & Software Development / 编程与软件开发

> Prompts for the most common AI use case: writing, reviewing, debugging, and explaining code. Designed for developers who want more than autocomplete.

---

## 场景描述 / Scenario

你用 AI 写代码，但不想让它吐出你一眼看不懂的 "黑箱代码"。你需要的是：可解释的实现、系统化的审查、不敷衍的 debug，以及能帮你建立心智模型的代码讲解。

---

## Prompt 1: 带推理链的代码生成 / Reasoning-First Code Generation

**适用场景：** 让 AI 写代码之前先讲清楚设计思路，避免 "给了代码但不知道为什么这样写"。

```
我需要你实现 [功能描述]。

但在此之前，请先输出：
1. 设计思路：你打算怎么解决这个问题？（3-5 句话）
2. 关键决策：为什么选这个方案而不是 [备选方案]？
3. 边界条件：哪些情况下这个实现会失效？

然后再输出代码。代码中关键决策处加注释说明 "为什么这样做"（而非 "做了什么"）。
```

**English version:**

```
I need you to implement [feature description].

But first, output:
1. Design approach: How do you plan to solve this? (3-5 sentences)
2. Key decisions: Why this approach over [alternative]?
3. Edge cases: Under what conditions will this implementation break?

Then output the code. Comment key decisions with "why this way" (not "what this does").
```

**Why it works:** 强制 AI 在写代码前先 "想一遍"，减少了 "代码看起来对但逻辑有漏洞" 的情况。"为什么这样做" 的注释要求让代码本身成为可维护的文档。See [`techniques/thinking-chain.md`](../techniques/thinking-chain.md).

---

## Prompt 2: 系统化代码审查 / Systematic Code Review

**适用场景：** 提交前自查或审查他人代码，不止看风格，更看逻辑和安全性。

```
请从以下四个维度审查这段代码，每个维度给出独立结论：

1. 正确性：逻辑是否有误？边界条件是否覆盖？
2. 安全性：是否存在注入、越权、敏感信息泄露等常见漏洞？
3. 性能：是否有 N+1 查询、不必要的循环、内存泄漏风险？
4. 可维护性：命名是否清晰？函数职责是否单一？是否有过度抽象？

对每个发现的问题，标注严重程度（阻塞/严重/建议）。
最后给出一个优先级排序的修复清单。
```

**English version:**

```
Review this code across four dimensions, with independent conclusions for each:

1. Correctness: Logic errors? Edge cases handled?
2. Security: Injection, auth bypass, sensitive data exposure?
3. Performance: N+1 queries, unnecessary loops, memory leak risks?
4. Maintainability: Clear naming? Single-responsibility functions? Over-engineering?

For each finding, label severity: BLOCKER / CRITICAL / SUGGESTION.
Output a priority-ordered fix checklist.
```

**Why it works:** 四个维度防止 AI 只关注表面（风格）而忽略实质（安全、逻辑）。严重程度标注让审查结果可直接用于 issue 管理。See [`techniques/critical-check.md`](../techniques/critical-check.md) and [`techniques/structured-output.md`](../techniques/structured-output.md).

---

## Prompt 3: 橡皮鸭 Debug / Rubber Duck Debugging

**适用场景：** 遇到 bug，需要 AI 帮你逐行排查而非直接给修复方案（直接给方案往往不治本）。

```
我遇到了一个 bug：[描述现象、报错信息]。

请不要直接给我修复方案。按以下步骤来：

1. 先复述你对这个 bug 的理解（让我确认问题描述是否准确）
2. 列出 3 个最可能的原因，按可能性排序
3. 对每个原因，设计一个最小验证方法（改哪里、怎么确认是不是这个原因）
4. 等我确认了根因，再提供修复方案

记住：我要的是排查过程，不是直接修。
```

**English version:**

```
I'm debugging: [describe symptoms, error messages].

Do NOT jump to a fix. Follow these steps:

1. Restate your understanding of the bug (let me confirm the problem description)
2. List the 3 most likely causes, ranked by probability
3. For each cause, design a minimal verification method (what to change, how to confirm)
4. Wait for me to confirm the root cause before suggesting a fix

Remember: I want the investigation process, not a quick fix.
```

**Why it works:** 很多 bug 的多轮排查比一次性修复更高效，但 AI 的默认行为是 "看到问题就给方案"。这个 prompt 强制 AI 扮演调试伙伴而非方案输出器。See [`techniques/role-persona.md`](../techniques/role-persona.md) and [`techniques/thinking-chain.md`](../techniques/thinking-chain.md).

---

## 注意事项 / Caveats

- AI 生成的代码需要人工审查，尤其是安全敏感和涉及数据库操作的代码
- 代码审查 prompt 适合 300 行以内的代码片段，更大的建议按模块拆分审查
- Rubber duck debug 的前提是你需要提供足够准确的 bug 描述，输入质量决定输出质量
- 不同 AI 模型的代码生成能力差异巨大，对同一个 prompt 的产出质量可能相差悬殊
