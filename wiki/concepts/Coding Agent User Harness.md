---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Harness engineering for coding agent users]]"
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
tags:
  - llm-wiki/concept
  - harness-engineering
  - coding-agents
  - user-harness
---
# Coding Agent User Harness

## 定义

Coding agent 用户侧工作支架（Coding Agent User Harness）是 coding agent 用户围绕特定代码库和团队工作流搭建的外层控制系统。它不同于模型本身，也不同于 agent 产品内置的 builder harness；它由用户可维护的 guides、tools、checks、review agents、hooks、docs 和监控组成。

## 为什么重要

同一个 coding agent 放进不同代码库会有不同可靠性。用户层 harness 把团队知道但模型未必知道的规则、架构、运行方式、质量标准和反馈机制外化出来，减少 review toil、提高系统质量，并避免把每次失败都当成一次性 prompt 问题。

## 来源支持的要点

- Böckeler 将 harness 分成三层：model，coding agent builder harness，以及 user harness。
- Builder harness 包括系统提示词、代码检索机制、编排系统等；user harness 是用户为自己系统放置的 feedforward/feedback controls。
- 一个好 user harness 的目标是提高首次生成正确率，并让更多问题在到达人类 review 前被自修正。
- 人类在这里的工作是 steering：根据反复出现的问题持续改进 guides 与 sensors。

- Bolin 访谈从 agent product builder 角度补充：用户/团队不仅要写 rules，还要优化新的 developer inner loop，例如是否把重复操作做成 skill、是否共享 skill、如何并行管理多个 agent workstreams。
- 这与 Böckeler 的 user harness 对齐：用户侧 harness 不只是 prompt，而是团队把重复反馈和工作流优化沉淀为可复用工具和规则。

- @affaan 的 Claude Code setup 把 user harness 具体化为 `~/.claude` 层：skills/commands、hooks、subagents、rules/memory、MCPs、plugins、statusline、editor integration、worktrees 和 tmux。
- 该来源强调“配置很多、启用很少”：user harness 不只是增加能力，也要主动管理上下文窗口和工具预算。
- Hooks 与 rules 的组合说明，用户侧 harness 可以从自然语言 guide 逐步升级为可执行 sensor / guardrail。

## 相关概念

- [[wiki/concepts/Context Engineering for Coding Agents|Context Engineering for Coding Agents]]

- [[wiki/concepts/Feedforward Guides|Feedforward Guides]]
- [[wiki/concepts/Feedback Sensors|Feedback Sensors]]
- [[wiki/concepts/Computational and Inferential Controls|Computational and Inferential Controls]]
- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Harnessability|Harnessability]]

- [[wiki/concepts/Claude Code Operating Harness|Claude Code Operating Harness]]
- [[wiki/concepts/MCP and Plugin Context Budget|MCP and Plugin Context Budget]]
- [[wiki/concepts/Parallel Agent Workflows|Parallel Agent Workflows]]

## 开放问题

- User harness 与 agent 产品/平台内置 harness 的责任边界如何划分？
- 哪些 user harness 工件应该进入仓库，哪些应该在 IDE、CI 或外部知识系统中？
- 如何度量 user harness 是否真的降低了 review toil？
