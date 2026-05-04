# Relay Brainstorm

> [English](#english) | [中文](#中文)

A multi-agent brainstorming framework that works with **any AI tool** — Claude Code, ChatGPT, Cursor, Kimi, Windsurf, and more.

---

## English

### What is it?

Relay Brainstorm turns a single prompt into a structured, multi-expert team discussion. Instead of one AI answer, you get coordinated debate between specialists — then a synthesized recommendation.

### Why?

- **Single-perspective bias** — LLMs give one answer. This forces multiple viewpoints.
- **No Devil's Advocate** — Ideas that survive challenge are stronger.
- **Structured output** — Formal recommendation with rationale, alternatives, and risks.

### Quick Start (Any AI Tool)

Copy this into any AI chat:

```
You are a multi-expert brainstorming coordinator. Discuss this topic by analyzing from 6 expert perspectives:

1. Tech Expert: feasibility, architecture, complexity
2. User Researcher: user needs, UX, pain points
3. Business Analyst: cost, ROI, market, competition
4. Creative Catalyst: cross-domain ideas, contrarian thinking
5. Devil's Advocate: challenge assumptions, find holes

Then synthesize all views into:
- Recommended plan (with rationale)
- Alternative plans
- Risk warnings
- Next steps

Topic: [YOUR TOPIC HERE]
```

### The 6 Expert Roles

| Role | Focus | Prompt File |
|------|-------|-------------|
| **Commander** | Strategy, outline, coordination | `prompts/commander.md` |
| **Tech Expert** | Feasibility, architecture | `prompts/tech-expert.md` |
| **User Researcher** | Needs, UX, pain points | `prompts/user-researcher.md` |
| **Business Analyst** | Cost, ROI, market | `prompts/business-analyst.md` |
| **Creative Catalyst** | Cross-domain ideas | `prompts/creative-catalyst.md` |
| **Devil's Advocate** | Challenge, stress-test | `prompts/devils-advocate.md` |

### Installation

#### For Claude Code

```bash
# macOS / Linux
git clone https://github.com/accaxx123/relay-brainstorm.git ~/.claude/skills/relay-brainstorm

# Windows (PowerShell)
git clone https://github.com/accaxx123/relay-brainstorm.git "$env:USERPROFILE\.claude\skills\relay-brainstorm"
```

Restart Claude Code, then type `/relay-brainstorm`.

#### For ChatGPT / Cursor / Kimi / Other Tools

1. Clone or download this repo
2. Open `workflow.md` for step-by-step instructions
3. Copy prompts from `prompts/` directory into your tool's custom instructions

### Project Structure

```
relay-brainstorm/
├── README.md                 # This file
├── workflow.md               # Universal workflow guide (any AI tool)
├── prompts/                  # Pure prompt files (no tool dependencies)
│   ├── commander.md
│   ├── tech-expert.md
│   ├── user-researcher.md
│   ├── business-analyst.md
│   ├── creative-catalyst.md
│   └── devils-advocate.md
├── references/               # Reference materials (checklists, templates)
│   ├── tech-checklist.md
│   ├── persona-template.md
│   ├── market-analysis.md
│   ├── brainstorming-techniques.md
│   ├── common-fallacies.md
│   └── integration-template.md
└── claude-code/              # Claude Code specific adapter
    └── SKILL.md
```

### Compatible Tools

| Tool | How to use |
|------|-----------|
| **Claude Code** | Clone to `~/.claude/skills/`, use `/relay-brainstorm` |
| **ChatGPT** | Paste prompts into custom instructions or chat |
| **Cursor** | Add prompts to `.cursorrules` or chat |
| **Kimi** | Paste prompts into system prompt |
| **Windsurf** | Add prompts to rules file |
| **Any LLM** | Use `workflow.md` as guide |

### Requirements

- Any LLM with long context (Claude, GPT-4, Gemini, etc.)
- For Claude Code: access to Opus and Sonnet models

### License

MIT

---

## 中文

### 这是什么？

Relay Brainstorm 把一个头脑风暴话题变成一场结构化的多专家团队讨论。你得到的不是单一视角，而是多个专家的辩论和最终综合方案。

### 为什么需要？

- **单一视角偏差** — LLM 倾向于给一个答案。这个框架强制多角度分析。
- **没有反驳者** — 能经受挑战的想法才是好想法。
- **结构化输出** — 正式的推荐方案，包含理由、备选方案和风险。

### 快速开始（任何 AI 工具）

把这段话粘贴到任何 AI 对话中：

```
你是一个多专家头脑风暴协调者。请从以下 6 个专家视角分析话题：

1. 技术专家：可行性、架构、实现复杂度
2. 用户研究员：用户需求、体验、痛点
3. 商业分析师：成本、收益、市场、竞争
4. 创意激发者：跨界联想、反直觉想法
5. 反驳者：挑战假设、找漏洞、压力测试

然后综合所有观点，输出：
- 推荐方案（带理由）
- 备选方案
- 风险提示
- 下一步行动

话题：[在这里填入你的话题]
```

### 6 个专家角色

| 角色 | 擅长领域 | Prompt 文件 |
|------|----------|------------|
| **总指挥** | 策略、大纲、协调 | `prompts/commander.md` |
| **技术专家** | 可行性、架构 | `prompts/tech-expert.md` |
| **用户研究员** | 需求、体验、痛点 | `prompts/user-researcher.md` |
| **商业分析师** | 成本、收益、市场 | `prompts/business-analyst.md` |
| **创意激发者** | 跨界联想 | `prompts/creative-catalyst.md` |
| **反驳者** | 挑战、压力测试 | `prompts/devils-advocate.md` |

### 安装

#### Claude Code 用户

```bash
# macOS / Linux
git clone https://github.com/accaxx123/relay-brainstorm.git ~/.claude/skills/relay-brainstorm

# Windows (PowerShell)
git clone https://github.com/accaxx123/relay-brainstorm.git "$env:USERPROFILE\.claude\skills\relay-brainstorm"
```

重启 Claude Code，输入 `/relay-brainstorm` 即可使用。

#### ChatGPT / Cursor / Kimi / 其他工具用户

1. 克隆或下载本仓库
2. 打开 `workflow.md` 查看分步指南
3. 从 `prompts/` 目录复制 prompt 到你工具的自定义指令中

### 项目结构

```
relay-brainstorm/
├── README.md                 # 本文件
├── workflow.md               # 通用工作流指南（适用任何 AI 工具）
├── prompts/                  # 纯 prompt 文件（无工具依赖）
│   ├── commander.md
│   ├── tech-expert.md
│   ├── user-researcher.md
│   ├── business-analyst.md
│   ├── creative-catalyst.md
│   └── devils-advocate.md
├── references/               # 参考资料（检查清单、模板）
│   ├── tech-checklist.md
│   ├── persona-template.md
│   ├── market-analysis.md
│   ├── brainstorming-techniques.md
│   ├── common-fallacies.md
│   └── integration-template.md
└── claude-code/              # Claude Code 专用适配层
    └── SKILL.md
```

### 兼容工具

| 工具 | 使用方式 |
|------|---------|
| **Claude Code** | 克隆到 `~/.claude/skills/`，输入 `/relay-brainstorm` |
| **ChatGPT** | 粘贴 prompt 到自定义指令或对话中 |
| **Cursor** | 添加 prompt 到 `.cursorrules` 或对话中 |
| **Kimi** | 粘贴 prompt 到系统提示中 |
| **Windsurf** | 添加 prompt 到 rules 文件 |
| **任何 LLM** | 参考 `workflow.md` 指南 |

### 环境要求

- 任何支持长上下文的 LLM（Claude、GPT-4、Gemini 等）
- Claude Code 用户需要 Opus 和 Sonnet 模型访问权限

### 许可证

MIT
