---
type: concept
status: draft
created: 2026-06-01
updated: 2026-06-03
aliases:
  - Parallel Claude workflows
  - Parallel agent workstreams
sources:
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
  - "[[wiki/sources/2026-06-03 A harness for every task dynamic workflows in Claude Code]]"
tags:
  - llm-wiki/concept
  - parallel-agents
  - worktrees
  - claude-code
---
# Parallel Agent Workflows

## 定义

Parallel Agent Workflows（并行智能体工作流）是同时运行多个 agent 会话或工作树来推进不同任务的模式。它需要明确任务不重叠程度、代码工作区隔离、上下文隔离和最终 review/merge 流程。

## 为什么重要

并行 agent 能提升吞吐，但也会放大冲突、重复工作、上下文切换和 review 负担。`/fork`、git worktrees、tmux 和状态线都是把并行执行变得可控的用户侧 harness 组件。

## 来源支持的要点

- Claude Code shorthand 来源建议 `/fork` 用于非重叠任务，git worktrees 用于重叠并行 Claude，避免同一 checkout 中互相覆盖。
- tmux 可用于长命令、前后端服务和日志观察，保持进程运行并支持用户 attach/detach。
- Bolin 访谈中也强调多 repo clone / 多 workstream 是 coding agent 带来的 developer inner loop 变化。
- Claude Code dynamic workflows 来源把并行推进进一步结构化：workflow 可 fan-out 子智能体、等待 barrier step，再综合结构化输出。
- 对迁移/重构任务，来源建议按 callsite、失败测试或模块拆分，在 worktree 中并行修复，再由独立 agent 对抗 review 和合并。

## 相关概念

- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]]
- [[wiki/concepts/Coding Agent User Harness|Coding Agent User Harness]]
- [[wiki/concepts/Subagent Scoping|Subagent Scoping]]
- [[wiki/concepts/Dynamic Workflows|Dynamic Workflows]]
- [[wiki/concepts/External Evaluator Agent|External Evaluator Agent]]
- [[wiki/entities/products/tmux|tmux]]

## 开放问题

- 并行 agent 的任务分配应由人类、planner subagent，还是 queue manager 决定？
- 多 worktree 输出如何做冲突检测和统一 review？
- 什么时候并行提升吞吐，什么时候只是制造 review overload？
- workflow 应如何自动限制并行度，避免资源耗尽或 review 成本超过收益？
