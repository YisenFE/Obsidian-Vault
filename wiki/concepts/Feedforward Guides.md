---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Harness engineering for coding agent users]]"
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
tags:
  - llm-wiki/concept
  - harness-engineering
  - feedforward
---
# Feedforward Guides

## 定义

生成前引导（Feedforward Guides）是在 coding agent 初始生成或执行前提供的指导、约束和能力入口，用来提高它“一开始就做对”的概率。

## 为什么重要

反馈能纠错，但越早避免错误，成本越低。Feedforward guides 把人类知识、架构约束、项目运行方式和工具能力提前放进 agent 可访问路径，减少无效探索和返工。

## 来源支持的要点

- Böckeler 的例子包括 AGENTS.md、skills、原则、CfRs、rules、reference docs、how-tos、language servers、CLIs/scripts 和 codemods。
- Feedforward guide 可以是 inferential 的，例如 coding conventions 或 review instructions；也可以是 computational 的，例如 bootstrap scripts、codemods、language server/code intelligence。
- Guide 的作用不是替代 feedback，而是把 agent 的初始生成拉向更高概率的正确区域。
- 在 change lifecycle 图中，feedforward examples 包括 LSP、architecture.md、/how-to-test skill、AGENTS.md、知识管理 MCP server、API docs skill。

- Claude Code shorthand 来源中的 skills、commands、rules folder、LSP plugins、codemaps、subagent descriptions 都是 feedforward guides 的具体形式。
- Rules 可按 security、coding-style、testing、git-workflow、agents、performance 等 concern 模块化，避免每次 prompt 重复说明。

## 相关概念

- [[wiki/concepts/Feedback Sensors|Feedback Sensors]]
- [[wiki/concepts/Coding Agent User Harness|Coding Agent User Harness]]
- [[wiki/concepts/Agent-readable Codebase|Agent-readable Codebase]]
- [[wiki/concepts/Repository as System of Record|Repository as System of Record]]

- [[wiki/concepts/Agent Rules and Memory|Agent Rules and Memory]]
- [[wiki/concepts/Codemaps for Agents|Codemaps for Agents]]

## 开放问题

- 哪些 guides 应该机器可执行，哪些只需要自然语言说明？
- Guide 太多时如何避免上下文污染、冲突和陈旧？
- 如何从重复 review 反馈中自动生成新的 guide？
