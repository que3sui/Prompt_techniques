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
