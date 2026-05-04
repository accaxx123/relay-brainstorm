# Relay Brainstorm

> [English](#english) | [中文](#中文)

---

## English

### What is Relay Brainstorm?

Relay Brainstorm is a **Claude Code skill** that turns a single brainstorming prompt into a structured, multi-expert team discussion. Instead of getting one perspective, you get a coordinated debate between specialists — then a synthesized recommendation.

### Why use it?

- **Single-perspective bias** — LLMs tend to give one answer. Relay Brainstorm forces multiple viewpoints.
- **No Devil's Advocate** — Ideas that survive challenge are stronger. The built-in Devil's Advocate agent stress-tests every consensus.
- **Structured output** — Not a freeform chat. The Commander agent produces a formal recommendation with rationale, alternatives, and risks.

### How it works

```
User provides a topic
       ↓
Commander: analyze topic → create discussion outline → select experts
       ↓
Commander: dispatch expert agents (multi-round)
       ↓  Commander reviews each expert's output
       ↓  Commander decides: more discussion or synthesize?
       ↓
Commander: integrate all perspectives → final recommendation
       ↓
Present to user → continue / implement / save
```

### The 6 Expert Roles

| Role | Focus | When summoned |
|------|-------|---------------|
| **Commander** | Strategy, outline, coordination, synthesis | Always — runs the discussion |
| **Tech Expert** | Feasibility, architecture, implementation complexity | When technical decisions matter |
| **User Researcher** | User needs, UX, pain points, adoption | When user impact matters |
| **Business Analyst** | Cost, ROI, market, competition | When business value matters |
| **Creative Catalyst** | Cross-domain ideas, contrarian thinking, breakthroughs | When discussion is stuck or needs fresh angles |
| **Devil's Advocate** | Challenge assumptions, find holes, stress-test | Before final decisions — always |

### Installation

```bash
# Clone into your Claude Code skills directory
git clone https://github.com/accaxx123/relay-brainstorm.git ~/.claude/skills/relay-brainstorm
```

### Usage

In Claude Code, type:

```
/relay-brainstorm
```

Or just describe your topic naturally. The skill triggers on keywords like: `brainstorm`, `头脑风暴`, `多角度`, `creative exploration`, `team discussion`.

### Example prompts

```
/relay-brainstorm 我们应该用 React 还是 Vue 来重构前端？

/relay-brainstorm How should we design the authentication system for our SaaS product?

/relay-brainstorm 我有一个创业想法，想从多个角度评估可行性
```

### What you get

After the discussion completes, the Commander outputs:

- **Recommended plan** — with step-by-step rationale
- **Consensus & disagreements** — what experts agreed on, what they didn't
- **Alternative plans** — if the primary plan isn't viable
- **Risk warnings** — what could go wrong
- **Next steps** — immediate actions you can take

### Architecture

```
relay-brainstorm/
├── SKILL.md                              # Skill definition (entry point)
├── README.md                             # This file
└── agents/
    ├── commander/                        # Commander agent (opus)
    │   ├── agent.md                      # Role definition
    │   └── examples/integration-template.md
    ├── tech-expert/                      # Tech Expert (sonnet)
    │   ├── agent.md
    │   └── references/tech-checklist.md
    ├── user-researcher/                  # User Researcher (sonnet)
    │   ├── agent.md
    │   └── references/persona-template.md
    ├── business-analyst/                 # Business Analyst (sonnet)
    │   ├── agent.md
    │   └── references/market-analysis.md
    ├── creative-catalyst/                # Creative Catalyst (sonnet)
    │   ├── agent.md
    │   └── references/brainstorming-techniques.md
    └── devils-advocate/                  # Devil's Advocate (sonnet)
        ├── agent.md
        └── references/common-fallacies.md
```

### Key principles

- **Commander has full authority** — decides which experts to summon, how many rounds, when to stop
- **No compression** — expert outputs are passed to Commander in full, never summarized
- **Commander must review** — every expert's output gets a quality score and evaluation
- **Devil's Advocate is mandatory** — consensus must be challenged before finalizing
- **User has final say** — Commander's plan is a recommendation, not a decision

### Requirements

- [Claude Code CLI](https://docs.anthropic.com/en/docs/claude-code)
- Access to Claude Opus and Sonnet models

### License

MIT

---

## 中文

### 什么是 Relay Brainstorm？

Relay Brainstorm 是一个 **Claude Code 技能**，把一个头脑风暴话题变成一场结构化的多专家团队讨论。你得到的不是单一视角，而是多个专家的辩论和最终综合方案。

### 为什么需要它？

- **单一视角偏差** — LLM 倾向于给一个答案。Relay Brainstorm 强制多角度分析。
- **没有反驳者** — 能经受挑战的想法才是好想法。内置的反驳者 agent 会压力测试每个共识。
- **结构化输出** — 不是随意聊天。总指挥 agent 会产出正式的推荐方案，包含理由、备选方案和风险。

### 工作流程

```
用户提供话题
       ↓
总指挥：分析话题 → 拟讨论大纲 → 确定需要哪些专家
       ↓
总指挥：按需调度专家 agent（多轮讨论）
       ↓  每个专家发言后，总指挥审查质量
       ↓  总指挥决定：继续讨论 or 整合结论
       ↓
总指挥：综合所有观点 → 输出最终方案
       ↓
展示给用户 → 继续深入 / 进入实施 / 保存结论
```

### 6 个专家角色

| 角色 | 擅长领域 | 何时被召唤 |
|------|----------|-----------|
| **总指挥** | 策略、大纲、协调、整合 | 始终在场 — 主持讨论 |
| **技术专家** | 可行性、架构、实现复杂度 | 需要做技术决策时 |
| **用户研究员** | 用户需求、体验、痛点、采纳度 | 需要理解用户视角时 |
| **商业分析师** | 成本、ROI、市场、竞争 | 需要评估商业价值时 |
| **创意激发者** | 跨界联想、反直觉创意、突破性思路 | 讨论陷入僵局或需要新角度时 |
| **反驳者** | 挑战假设、找漏洞、压力测试 | 做最终决策前 — 必须召唤 |

### 安装

```bash
# 克隆到 Claude Code 技能目录
git clone https://github.com/accaxx123/relay-brainstorm.git ~/.claude/skills/relay-brainstorm
```

### 使用方式

在 Claude Code 中输入：

```
/relay-brainstorm
```

或者直接描述你的话题，技能会在检测到关键词时自动触发：`brainstorm`、`头脑风暴`、`多角度`、`创意探索`、`团队讨论`。

### 示例

```
/relay-brainstorm 我们应该用 React 还是 Vue 来重构前端？

/relay-brainstorm How should we design the authentication system for our SaaS product?

/relay-brainstorm 我有一个创业想法，想从多个角度评估可行性
```

### 你会得到什么

讨论结束后，总指挥会输出：

- **推荐方案** — 带有逐步推理的详细方案
- **共识与分歧** — 专家们一致认同的点，以及存在争议的点
- **备选方案** — 如果主方案不可行的替代路径
- **风险提示** — 可能出问题的地方
- **下一步行动** — 你马上可以做的 1-2 件事

### 项目结构

```
relay-brainstorm/
├── SKILL.md                              # 技能定义（入口文件）
├── README.md                             # 本文件
└── agents/
    ├── commander/                        # 总指挥（opus 模型）
    │   ├── agent.md                      # 角色定义
    │   └── examples/integration-template.md
    ├── tech-expert/                      # 技术专家（sonnet 模型）
    │   ├── agent.md
    │   └── references/tech-checklist.md
    ├── user-researcher/                  # 用户研究员（sonnet 模型）
    │   ├── agent.md
    │   └── references/persona-template.md
    ├── business-analyst/                 # 商业分析师（sonnet 模型）
    │   ├── agent.md
    │   └── references/market-analysis.md
    ├── creative-catalyst/                # 创意激发者（sonnet 模型）
    │   ├── agent.md
    │   └── references/brainstorming-techniques.md
    └── devils-advocate/                  # 反驳者（sonnet 模型）
        ├── agent.md
        └── references/common-fallacies.md
```

### 核心原则

- **总指挥有完全决策权** — 调度哪个专家、讨论几轮、何时结束，都由总指挥决定
- **不要压缩专家输出** — 完整传递给总指挥，不做摘要
- **总指挥必须审查** — 每个专家的发言都会被打分和评价
- **反驳者必须参与** — 最终决策前必须挑战共识
- **用户拥有最终决定权** — 总指挥的方案只是建议

### 环境要求

- [Claude Code CLI](https://docs.anthropic.com/en/docs/claude-code)
- 可使用 Claude Opus 和 Sonnet 模型

### 许可证

MIT
