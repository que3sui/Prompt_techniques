# Structured Output Control / 结构化输出控制

> Techniques for making AI produce consistently formatted output — JSON, tables, Markdown templates, and custom schemas. Turns "sometimes it works" into "always works."

---

## 场景描述 / Scenario

你不只是想让 AI 输出 "一段文字"。你需要 JSON 给程序解析、表格给人对比、固定模板给下游工具消费。默认输出格式不可控是 AI 使用中最常见的痛点——本页提供系统化的解决方案。

---

## 技巧 / Techniques

### 1. 显式格式描述 / Explicit Schema

**适用场景：** 需要 JSON/YAML 等结构化数据，且字段较多。

**核心原则：** 不要让 AI "猜" 你的 schema。写出来，每个字段说明类型和含义。

**Prompt 模板：**

````
请输出 JSON，格式如下：

{
  "field_name": "字段含义 (类型: string/number/boolean/array)",
  ...
}

规则：
- 严格遵守字段名和类型
- 如果某个字段没有对应数据，用 null 而非省略该字段
- 不要输出任何 JSON 之外的文字
- 用 ```json 代码块包裹输出

数据要求：
[描述你需要提取或生成的内容]
````

**English version:**

````
Output JSON in this schema:

{
  "field_name": "description (type: string/number/boolean/array)",
  ...
}

Rules:
- Strictly follow field names and types
- Use null for missing data, never omit fields
- Output ONLY the JSON, no surrounding text
- Wrap in ```json code block

Data requirements:
[Describe what to extract or generate]
````

---

### 2. 表格模板 / Table Template

**适用场景：** 需要 AI 用表格对比、列举或总结信息。

**Prompt 模板：**

```
请用 Markdown 表格输出。表头固定为：

| 列1名称 | 列2名称 | 列3名称 |

要求：
- 每行信息密度一致，不要有的行写三句话有的只写一个词
- 表格后可以有一句总结性备注，但不超过一句话
- 如果对比类表格，确保每列的对比维度一致

内容：
[你的需求]
```

**English version:**

```
Output as a Markdown table with fixed headers:

| Column 1 | Column 2 | Column 3 |

Requirements:
- Consistent information density per row
- One optional summary sentence after the table, no more
- For comparison tables, ensure consistent comparison dimensions per column

Content:
[Your request]
```

---

### 3. 逐段模板填充 / Section-by-Section Template

**适用场景：** 需要 AI 按固定章节结构输出长篇内容，每个章节有明确定义。

**Prompt 模板：**

```
请严格按照以下章节结构输出，不要增减章节：

## 摘要 (2-3 句话)

## 核心要点 (3-5 个 bullet point)

## 详细分析
- 背景
- 关键因素
- 风险与不确定性

## 行动建议 (具体、可操作)

规则：如果某个章节确实没有内容可写，写 "本节不适用" 并说明原因，不要直接跳过。
```

**English version:**

```
Output strictly following this section structure. Do not add or remove sections:

## Summary (2-3 sentences)

## Key Points (3-5 bullet points)

## Detailed Analysis
- Background
- Key Factors
- Risks & Uncertainties

## Actionable Recommendations (specific, concrete)

Rule: If a section genuinely has no content, write "Not applicable" and explain why — never silently skip a section.
```

---

## 为什么有效 / Why It Works

结构化输出的关键是降低 AI 的 "自由度"。"输出 JSON" 是模糊指令——AI 不知道自己决定 schema 是否合适。给出完整 schema 后，AI 的任务从 "创造结构+填充内容" 简化为 "填充内容"，错误率大幅下降。表格模板同理：固定表头消除了结构决策，AI 只需按列填内容。

Related techniques:

- [`techniques/few-shot.md`](few-shot.md) — 用示例锚定格式是最强的结构控制手段
- [`techniques/output-quality.md`](output-quality.md) — 格式是信息密度的载体

---

## 注意事项 / Caveats

- JSON 输出在 token 消耗上比纯文本高约 20-30%，高频调用时需要考虑成本
- 复杂嵌套 JSON 的错误率显著上升 —— 尽量用扁平结构
- 不同模型对格式遵循的能力差异很大，如果切换模型，先测一下格式一致性
- 表格过宽（6+ 列）时 AI 可能截断或合并列，控制在 4 列以内最稳
