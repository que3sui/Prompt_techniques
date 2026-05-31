# Auto Prompt Harvest — 自动 Prompt 收割系统

## Problem Statement

**How Might We:** 在日常对话中自动捕获高质量 prompt-answer 对，定期横向比对，将最优 prompt 按"场景先行→技巧后置"工作流自动更新到 Prompt_techniques 仓库？

## Recommended Direction

**两个组件，会话结束 hook 统一驱动：**

```
会话结束
  │
  ├─ Hook: 保存 transcript → 触发后台分析子进程（非阻塞）
  │
  └─ 后台子进程 (claude -p):
       ├─ Step 1: 逐对评分，存 inbox/
       ├─ Step 2: inbox ≥ 阈值? → 横向比对
       └─ Step 3: 选最优 → 场景→技巧工作流 → 入仓 → commit+push
```

### 为什么这个结构

1. **Hook 只做两件事：** 保存原始数据 + 触发后台。不阻塞会话结束。
2. **子进程用 `claude -p` 跑：** 评分和提取需要 Claude 的判断力，不能用脚本硬编码规则。
3. **会话结束 = 定期触发器：** 不需要 cron、不需要 Windows Task Scheduler，每次用完 Claude 就自动积累。
4. **inbox 做阈值门控：** 未处理的 JSON 记录计为 inbox。满 N 条（建议 15-20）触发一次横向比对，避免每次都跑的 token 浪费。

## File Structure

```
~/.claude/prompts/
├── transcripts/                  # 原始会话 transcript，按日期命名
│   └── 2026-06-01-session.md
├── inbox/                        # 未处理的评分记录 (JSON)
│   ├── rec-001.json
│   ├── rec-002.json
│   └── ...
├── archive/                      # 已处理的评分记录，分析完成后移入
│   └── 2026-06-01-batch/
│       ├── rec-001.json
│       ├── rec-002.json
│       └── ...
└── analysis.md                   # 最近一次横向比对的结果摘要
```

### JSON 记录结构

```json
{
  "id": "rec-20260601-a3f2",
  "date": "2026-06-01",
  "session_transcript": "2026-06-01-session.md",
  "prompt": "完整的用户 prompt 原文",
  "answer_summary": "AI 回答的摘要（前 300 字）",
  "full_answer": "完整的 AI 回答",
  "score": 8,
  "score_reasoning": "role-persona 设定精准，thinking-chain 要求让回答深入，可复用性强",
  "tags": ["role-persona", "thinking-chain", "academic"],
  "techniques_matched": ["role-persona", "thinking-chain", "output-quality"],
  "scenario": "academic",
  "repo_worthy": true
}
```

## Session-End Hook

位置：`~/.claude/settings.json` 中的 hooks 配置

```json
{
  "hooks": {
    "SessionEnd": [
      {
        "matcher": "",
        "command": "bash ~/.claude/scripts/auto-harvest.sh"
      }
    ]
  }
}
```

Hook 脚本 `~/.claude/scripts/auto-harvest.sh`：

```bash
#!/bin/bash
PROMPTS_DIR="$HOME/.claude/prompts"
TRANSCRIPT_DIR="$PROMPTS_DIR/transcripts"
PROJECT_DIR="E:/AlphaLab/prompt_technique"

# 1. 保存 transcript（从环境变量或 stdin 获取）
DATE=$(date +%Y-%m-%d)
TRANSCRIPT_FILE="$TRANSCRIPT_DIR/$DATE-session.md"
cat > "$TRANSCRIPT_FILE"  # Claude Code passes transcript via stdin

# 2. 后台触发分析子进程（非阻塞）
nohup claude -p \
  --project "$PROJECT_DIR" \
  --prompt "$(cat $PROJECT_DIR/.claude/prompts/analyze-prompt.md)" \
  --input-file "$TRANSCRIPT_FILE" \
  > "$PROMPTS_DIR/last-analysis.log" 2>&1 &
```

## Analysis Script Prompt

位置：`E:/AlphaLab/prompt_technique/.claude/prompts/analyze-prompt.md`

这个 prompt 是分析子进程的核心指令，内容需要你确认后单独写。

大致结构：

1. 读取 transcript，提取所有 prompt-answer 对
2. 对每个对评分（1-10），基于技巧库标准
3. 存为 JSON 到 `~/.claude/prompts/inbox/`
4. 若 inbox 满 20 条 → 横向比对，选出 Top 3
5. 对 Top 3 走场景先行→技巧后置工作流，写入仓库
6. 将处理过的记录移到 archive/

## MVP Scope

- [x] Hook 保存 transcript
- [ ] 分析子流程：评分 + 存 JSON
- [ ] 横向比对机制（inbox 阈值触发）
- [ ] 自动入仓：场景先行 → 技巧后置 → commit push
- [ ] Hook 脚本 + 分析 prompt 文件就位

## Not Doing (and Why)

- **实时评分** — 复杂度高，打断对话流。会话结束回顾足够。
- **评分校准/模型微调** — over-engineering。Claude 主观评分 + 人工偶尔看一眼 archive 就能保持质量。
- **Web UI / Dashboard** — 轻量即可。JSON 文件 + analysis.md 足够透明。
- **支持非 Claude 的 transcript** — MVP 只面向 Claude Code 自己的会话。
- **定时 cron 触发** — 不需要。会话结束就是最自然的触发器。

## Key Assumptions to Validate

- [ ] Claude Code 的 SessionEnd hook 确实会传递 transcript 内容（需验证，不同版本行为可能不同）
- [ ] 后台 `nohup claude -p` 不会因为父进程退出而被 kill
- [ ] `claude -p` 可以读取并写入 `~/.claude/prompts/` 目录（权限无问题）
- [ ] 20 条阈值合理：太低浪费 token，太高积累太久

## Open Questions

- Hook 的 transcript 格式是什么？可能需要解析适配
- 是否需要在 analysis prompt 里限制每次分析的最大 token 消耗？
- 仓库已有相关场景时，自动入仓是追加还是合并到已有文件？
