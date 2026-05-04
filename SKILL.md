---
name: relay-brainstorm
description: >-
  Use when the user wants multi-perspective brainstorming, creative ideation,
  or structured exploration through a coordinated AI team discussion.
  Trigger on: brainstorm, 头脑风暴, 多角度, 讨论, 探索方案, 团队讨论, creative exploration.
---

# Relay Brainstorm — 多 Agent 头脑风暴团队

一个总指挥协调多个专家 agent，围绕话题进行动态讨论，最终产出结构化方案。

## 角色

| 角色 | 职责 | Agent 文件 | 参考资料 |
|------|------|-----------|---------|
| 总指挥 (Commander) | 拟大纲、定方向、审查发言、调度专家、整合结论 | `./agents/commander/agent.md` | `./agents/commander/examples/` |
| 技术专家 (Tech Expert) | 技术可行性、架构方案、实现难度 | `./agents/tech-expert/agent.md` | `./agents/tech-expert/references/` |
| 用户研究员 (User Researcher) | 用户需求、体验、痛点 | `./agents/user-researcher/agent.md` | `./agents/user-researcher/references/` |
| 商业分析师 (Business Analyst) | 成本、收益、市场竞争 | `./agents/business-analyst/agent.md` | `./agents/business-analyst/references/` |
| 创意激发者 (Creative Catalyst) | 跨界联想、反直觉创意 | `./agents/creative-catalyst/agent.md` | `./agents/creative-catalyst/references/` |
| 反驳者 (Devil's Advocate) | 挑战假设、找漏洞、压力测试 | `./agents/devils-advocate/agent.md` | `./agents/devils-advocate/references/` |

## 流程

```
用户提供话题
    ↓
总指挥: 分析话题 → 拟讨论大纲 → 确定需要哪些专家
    ↓
总指挥: 按需召唤专家 agent（可能多轮）
    ↓ 每个专家发言后，总指挥审查质量
    ↓ 总指挥决定是否需要更多讨论
    ↓
总指挥: 整合所有观点 → 输出最终方案
    ↓
展示给用户 → 继续讨论 / 进入实施 / 保存
```

## 执行步骤

### Step 1: 收集话题

如果用户没有提供话题，用 AskUserQuestion 收集。
如果有项目上下文，读取关键文件（README、CLAUDE.md 等）。

### Step 2: 创建任务

用 TaskCreate 创建任务：
1. "总指挥：拟讨论大纲" — in_progress
2. "讨论进行中" — pending（由总指挥动态管理子任务）
3. "总指挥：整合最终方案" — pending

### Step 3: Dispatch 总指挥

读取 `agents/commander/agent.md`。

用 Agent 工具 dispatch 总指挥：
- model: opus（需要最强推理能力）
- prompt: agent.md 内容 + 话题 + 项目上下文 + 可用专家列表

总指挥会返回：
- 讨论大纲
- 需要召唤的专家列表及顺序
- 每个专家的讨论焦点

### Step 4: 按总指挥指示召唤专家

根据总指挥的指示，依次 dispatch 专家 agent：
- 读取对应的 `agents/[角色]/agent.md`
- 用 Agent 工具 dispatch，model: sonnet
- prompt: agent.md 内容 + 话题 + 讨论大纲 + 该专家的焦点问题 + 之前专家的发言（如有）

收到专家输出后：
- 创建新任务记录该专家的发言
- 将专家输出传回给总指挥审查

### Step 5: 总指挥审查并决策

将专家输出传给总指挥，总指挥会返回：
- 对该专家发言的评价
- 是否需要更多讨论
- 下一步：召唤哪个专家 / 进入整合 / 需要补充信息

根据总指挥的决策继续调度。

### Step 6: 总指挥整合

当总指挥决定讨论充分后，让它输出最终方案：
- 推荐方案（带理由）
- 备选方案
- 风险提示
- 下一步建议

### Step 7: 展示结果

展示给用户，用 AskUserQuestion 询问：
1. 继续深入讨论某个方向
2. 进入实施（调用 writing-plans）
3. 保存结论

## 关键原则

- **总指挥有完全决策权** — 调度哪个专家、讨论几轮、何时结束，都由总指挥决定
- **不要压缩专家输出** — 完整传递给总指挥，不要摘要
- **总指挥必须审查** — 每个专家发言后，总指挥必须给出评价和下一步指示
- **反驳者很重要** — 总指挥应该在适当时机召唤反驳者挑战共识
- **尊重用户** — 最终决定权在用户，总指挥的方案只是建议

## Agent 定义

每个 agent 有独立文件夹，包含 `agent.md`（YAML frontmatter + 结构化 body）和可选的 references/examples。

- `./agents/commander/agent.md` — 总指挥（model: opus）
- `./agents/tech-expert/agent.md` — 技术专家（model: sonnet）
- `./agents/user-researcher/agent.md` — 用户研究员（model: sonnet）
- `./agents/business-analyst/agent.md` — 商业分析师（model: sonnet）
- `./agents/creative-catalyst/agent.md` — 创意激发者（model: sonnet）
- `./agents/devils-advocate/agent.md` — 反驳者（model: sonnet）

### 参考资料

| Agent | References | 用途 |
|-------|-----------|------|
| 总指挥 | `examples/integration-template.md` | 整合方案的输出模板 |
| 技术专家 | `references/tech-checklist.md` | 技术分析检查清单 |
| 用户研究员 | `references/persona-template.md` | 用户画像构建模板 |
| 商业分析师 | `references/market-analysis.md` | 市场分析框架 |
| 创意激发者 | `references/brainstorming-techniques.md` | 创意激发技巧库 |
| 反驳者 | `references/common-fallacies.md` | 常见逻辑谬误清单 |
