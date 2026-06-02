# Few-Shot Prompting / 少样本示例驱动

> Give the AI 2-3 input→output examples before your actual request. Few-shot examples are one of the most reliable ways to control output format, style, and quality — often more effective than explicit instructions alone.

---

## 场景描述 / Scenario

当你需要 AI 输出特定格式、风格或质量水平时，光靠文字描述往往不够精确。提供 2-3 个示例可以让 AI 直接 "看到" 你想要什么，比一百字的描述更有效。适用于格式控制、风格模仿、质量锚定等场景。

---

## 技巧 / Techniques

### 1. 格式锚定 / Format Anchoring

**适用场景：** 需要 AI 按特定结构输出（JSON、表格、特定模板）。

**Prompt 模板：**

```
请按照以下示例的格式输出。注意：不是复制内容，而是复制结构。

示例 1:
[完整的输入→输出示例，展示你期望的结构]

示例 2:
[另一个示例，覆盖边缘情况]

现在，请对以下内容按同样格式处理：
[你的实际输入]
```

**English version:**

```
Follow the format shown in the examples below. Match the structure, not the content.

Example 1:
[Complete input→output pair showing desired structure]

Example 2:
[Another example, covering an edge case]

Now process the following in the same format:
[Your actual input]
```

---

### 2. 质量锚定 / Quality Anchoring

**适用场景：** 你希望 AI 输出达到一定深度或质量水平，用示例来 "设定标准"。

**Prompt 模板：**

```
以下是我期望的分析深度示例。后续所有分析请保持同等深度。

示例（期望的质量水平）：
[一段高质量的分析，展示你期望的深度、细节程度和推理方式]

请在同等深度下分析：
[你的实际问题]
```

**English version:**

```
Below is an example of the analysis depth I expect. Match this depth for all subsequent responses.

Example (target quality level):
[A high-quality analysis showing desired depth, detail, and reasoning style]

Now analyze at the same depth:
[Your actual question]
```

---

### 3. 反例锚定 / Contrastive Examples

**适用场景：** 当"好"难以定义时，给出好和坏的对比示例，让边界更清晰。

**Prompt 模板：**

```
以下是我认为"好"和"不够好"的对比示例。请以"好"的标准输出。

不够好（不要这样）：
[一个不够好的示例，标注为什么不够好]

好（要这样）：
[一个好的示例，标注为什么好]

现在处理：
[你的实际输入]
```

**English version:**

```
Below are contrastive examples. Follow the "good" standard.

Not good enough (avoid):
[A subpar example, with notes on why it falls short]

Good (aim for this):
[A good example, with notes on what makes it work]

Now process:
[Your actual input]
```

---

## 为什么有效 / Why It Works

少样本示例利用了 AI 的模式匹配能力。相比于自然语言指令（需要 AI "理解"你的意图后再执行），示例直接展示了输入→输出的映射模式，AI 只需 "匹配并复制" 这种模式。这绕过了指令理解中的模糊性和信息损失。格式锚定尤其有效，因为 AI 对结构模式的捕获比对话义理解更精确。

Related techniques:

- [`techniques/role-persona.md`](role-persona.md) — 角色设定可以和示例组合使用，角色定义 "谁在写"，示例定义 "写成什么样"
- [`techniques/output-quality.md`](output-quality.md) — 示例是最直接的质量锚定方式

---

## 注意事项 / Caveats

- 示例不要太多。2-3 个通常足够，超过 5 个可能让 AI 过拟合到示例的具体内容而非抽象模式
- 示例中的事实错误会被 AI 模仿 —— 确保示例本身是正确的
- 对于创意类任务，示例可能过度约束输出空间，用反例锚定比正例更安全
- token 开销：示例会占用上下文窗口，长示例需要权衡成本
