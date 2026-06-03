---
type: organization
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
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

## 相关页面

- [[wiki/entities/products/Claude Agent SDK|Claude Agent SDK]]
- [[wiki/entities/products/Claude Code|Claude Code]]
- [[wiki/entities/products/Claude Opus 4.6|Claude Opus 4.6]]
- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/themes/长时程智能体工作流|长时程智能体工作流]]
- [[wiki/syntheses/Anthropic 长时程 harness 演化|Anthropic 长时程 harness 演化]]
