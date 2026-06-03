---
type: concept
status: draft
created: 2026-06-01
updated: 2026-06-01
aliases:
  - Claude Code user harness
  - Claude Code setup harness
sources:
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
tags:
  - llm-wiki/concept
  - claude-code
  - user-harness
---
# Claude Code Operating Harness

## 定义

Claude Code Operating Harness（Claude Code 操作支架）是用户围绕 Claude Code 配置的一整套日常运行环境：skills/commands、hooks、subagents、rules/memory、MCPs、plugins、editor、worktree/tmux、statusline 和 CI review 等共同构成可复用、可观察、可约束的工作流。

## 为什么重要

Claude Code 本身只是 agent 产品；真正决定高吞吐和稳定性的，是用户如何把重复流程、上下文入口、权限边界、自动检查、并行隔离和编辑器观察面组合起来。该来源把 user harness 从抽象 guides/sensors 落到 `~/.claude` 配置和日常命令层。

## 来源支持的要点

- 文章把配置分为 skills/commands、hooks、subagents、rules/memory、MCPs、plugins、parallel workflows、editor integration、statusline。
- 其核心原则不是“工具越多越好”，而是像 fine-tuning 一样小心调参：禁用不用的 MCP/plugins，保持 context window 健康。
- Workflows 可以被串联，例如 `/refactor-clean` → `/test-coverage` → `/e2e`，把复杂任务变成短语化命令。
- Hooks、rules、subagents 和 plugins 把重复提醒、检查和 delegation 变成自动结构，而不是每次手写 prompt。

## 相关概念

- [[wiki/concepts/Coding Agent User Harness|Coding Agent User Harness]]
- [[wiki/concepts/Claude Code Hooks|Claude Code Hooks]]
- [[wiki/concepts/Subagent Scoping|Subagent Scoping]]
- [[wiki/concepts/MCP and Plugin Context Budget|MCP and Plugin Context Budget]]
- [[wiki/concepts/Parallel Agent Workflows|Parallel Agent Workflows]]
- [[wiki/concepts/Agent Rules and Memory|Agent Rules and Memory]]

## 开放问题

- 哪些配置属于个人偏好，哪些应进入项目或团队共享？
- Claude Code operating harness 的最小可行配置是什么？
- 如何避免配置过度复杂化，反而消耗上下文和维护成本？
