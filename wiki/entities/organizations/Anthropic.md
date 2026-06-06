---
type: organization
status: draft
created: 2026-05-29
updated: 2026-06-05
sources:
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
  - "[[wiki/sources/2026-06-03 A harness for every task dynamic workflows in Claude Code]]"
  - "[[wiki/sources/2026-06-06 Agents that remember]]"
tags:
  - llm-wiki/entity/organization
  - anthropic
---
# Anthropic

## 在本 wiki 中的角色

Anthropic 是 Claude、[[wiki/entities/products/Claude Agent SDK|Claude Agent SDK]]、[[wiki/entities/products/Claude Code|Claude Code]] 背后的组织，也是两篇长时程 agent harness 来源的发布方。

## 来源支持的要点

- [[wiki/sources/2026-05-28 Effective harnesses for long-running agents|Effective harnesses for long-running agents]] 描述 Anthropic 用 Claude Agent SDK 做跨多个 context window 的实验。
- 该来源把长时程 agent 可靠性视为环境与交接问题：初始脚手架、显式 feature requirements、progress notes、git history 和端到端测试。
- [[wiki/sources/2026-05-28 Harness design for long-running application development|Harness design for long-running application development]] 将该模式扩展为用于前端设计和 full-stack 应用生成的 planner/generator/evaluator 多智能体 harness。
- 后续来源强调 evaluator 校准、Playwright 驱动的 QA，以及随模型能力提升定期简化 harness。

- [[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code|The Shorthand Guide to Everything Claude Code]] 是第三方用户经验来源，围绕 Anthropic 的 Claude Code 产品整理个人配置实践；其中提到 Anthropic x Forum Ventures hackathon，但核心价值是 Claude Code user harness。
- [[wiki/sources/2026-06-03 A harness for every task dynamic workflows in Claude Code|A harness for every task]] 是 Claude blog 官方来源，介绍 Claude Code dynamic workflows：按任务生成 JavaScript 多智能体 harness，并用独立上下文、模型路由、worktree 隔离和对抗验证处理复杂任务。
- [[wiki/sources/2026-06-06 Agents that remember|Agents that remember]] 是 Claude workshop transcript，介绍 Claude Managed Agents 的 memory stores 与 dreaming：用文件系统式 memory 跨 session 持久化，再用异步多智能体 harness 整理长期记忆。

## 相关页面

- [[wiki/entities/products/Claude Agent SDK|Claude Agent SDK]]
- [[wiki/entities/products/Claude Code|Claude Code]]
- [[wiki/entities/products/Claude Managed Agents|Claude Managed Agents]]
- [[wiki/entities/products/Claude Platform|Claude Platform]]
- [[wiki/entities/products/Claude Opus 4.6|Claude Opus 4.6]]
- [[wiki/entities/products/Claude Opus 4.7|Claude Opus 4.7]]
- [[wiki/entities/products/Claude Opus 4.8|Claude Opus 4.8]]
- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Dynamic Workflows|Dynamic Workflows]]
- [[wiki/concepts/Agent Memory Stores|Agent Memory Stores]]
- [[wiki/concepts/Dreaming for Agent Memory|Dreaming for Agent Memory]]
- [[wiki/themes/长时程智能体工作流|长时程智能体工作流]]
- [[wiki/syntheses/Anthropic 长时程 harness 演化|Anthropic 长时程 harness 演化]]
