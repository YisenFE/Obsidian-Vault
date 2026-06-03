---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
  - "[[wiki/sources/2026-06-01 Using Goals in Codex]]"
tags:
  - llm-wiki/concept
  - agent-memory
  - session-handoff
  - long-running-agents
---
# Agent Memory and Session Handoff

## 定义

智能体记忆与跨会话交接（Agent Memory and Session Handoff）指长时程 agent 在多个离散上下文窗口或多 agent 阶段之间传递工作状态的机制。它不等同于模型内部记忆，而是把目标、近期进展、未完成事项、运行方式、验证结果和下一步计划外化成后续 agent 能快速读取的工件。

## 为什么重要

长任务通常无法在一个 context window 内完成。若下一轮 agent 不知道上一轮做了什么，就会重复摸索、误判完成度，或在半成品基础上继续扩大破坏。显式交接把“新人接班”问题转化为可读、可验证、可恢复的环境问题。

## 来源支持的要点

- Anthropic 早期文章把 long-running agent 的核心挑战描述为：每个新 session 默认没有上一轮记忆。
- Context compaction 有帮助，但不能稳定传递清晰的下一步指令或未完成状态。
- 早期方案使用 `claude-progress.txt` 与 git history 作为主要交接物，让新 session 快速理解近期工作。
- Coding agent 每轮开始要读取 progress file、git log、feature list，并运行基础端到端测试，先确认代码库没有遗留破坏。
- 每轮结束要写 descriptive commit 与 progress update，使下一轮可以恢复工作状态或回滚错误。
- 后续 harness design 文章进一步区分 [[wiki/concepts/Context Reset vs Compaction|Context Reset vs Compaction]]：reset 给新 agent clean slate，但要求 handoff artifact 足够完整。
- Planner/generator/evaluator 版本通过文件通信和 [[wiki/concepts/Sprint Contract|Sprint Contract]] 在 agent 阶段之间传递状态，而不只是跨时间 session 传递状态。

- NLAH 论文把 handoff 作为 IHR prototype 的主要弱点：parent-child execution 下 Information Handoff Recall 明显低于直接上下文 prompt，说明跨 agent 边界的信息传递需要更强结构。
- 同一论文的 RQ3 显示 [[wiki/concepts/File-backed State|File-backed State]] 在 SWE 和 OSWorld 上均提升 performance，支持“把关键状态落到文件”比只靠上下文更稳。

- Bolin 访谈提到 Codex 仍在探索 memory 与 context connectors：每次新 conversation 从空状态开始，因此 memory、`AGENTS.md` 和 context stuffing 都是在帮助模型快速进入状态。
- 访谈也提示未来 agent 可能跨机器、多子 agent 协作；这会把 handoff 从单 repo/session 问题扩展成 agent network 问题。

- LangChain Anatomy 来源把 filesystem + git 视为跨 session 工作追踪的基础：长任务会产生大量 token，文件系统持久保存工作，git 让新 agent 通过历史快速理解项目。
- 对多 agent 协作，文件系统也可以成为 shared ledger（共享账本）：不同 agent 和人类通过文件协调进展。

- Claude Code shorthand 来源中的 rules/memory、statusline、checkpoints、`/rewind`、`/compact` 和 tmux session 都是个人使用层面的状态管理工具。
- Git worktrees 和 `/fork` 让多个 Claude 会话保持独立状态，减少并行工作互相污染。

- Codex Goals 来源说明 Goal 是 thread-scoped durable state：它能跨 turn 保存 objective/status/budget/usage，但不等于 global memory 或 project-level instruction。
- 这给 memory 分层提供了一个中间层：比单轮 prompt 持久，比项目记忆更局部，绑定当前 thread 的证据轨迹。

## 相关概念

- [[wiki/concepts/File-backed State|File-backed State]]
- [[wiki/concepts/Intelligent Harness Runtime|Intelligent Harness Runtime]]
- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Repository as System of Record|Repository as System of Record]]
- [[wiki/concepts/Agent-readable Codebase|Agent-readable Codebase]]
- [[wiki/concepts/Self-verification|Self-verification]]
- [[wiki/concepts/Context Reset vs Compaction|Context Reset vs Compaction]]

- [[wiki/concepts/Filesystem as Harness Primitive|Filesystem as Harness Primitive]]
- [[wiki/concepts/Ralph Loop|Ralph Loop]]

- [[wiki/concepts/Parallel Agent Workflows|Parallel Agent Workflows]]
- [[wiki/concepts/Agent Rules and Memory|Agent Rules and Memory]]

- [[wiki/concepts/Codex Goals|Codex Goals]]

## 开放问题

- IHR/NLAH 这类 parent-child runtime 中，handoff artifact 应如何记录 provenance、scope 和遗漏风险？

- 交接文件应该是一份 `progress.txt`、结构化 JSON，还是进入正式 issue/plan 系统？
- 哪些状态应由 git history 表达，哪些应由 progress note、sprint contract 或 evaluator log 表达？
- Session handoff 与长期 memory store 的边界在哪里？
