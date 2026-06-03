---
type: concept
status: draft
created: 2026-05-29
updated: 2026-06-03
aliases:
  - Harness
  - Agent = Model + Harness
sources:
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
  - "[[wiki/sources/2026-06-03 A harness for every task dynamic workflows in Claude Code]]"
tags:
  - llm-wiki/concept
  - agent-harness
  - harness-engineering
---
# Agent Harness

## 定义

智能体工作支架（Agent Harness）是模型之外让智能体能行动、观察、记忆、验证、恢复和协作的系统层。LangChain 用 “Agent = Model + Harness” 概括：模型提供智能，harness 把智能接入文件系统、工具、沙箱、上下文管理、状态和反馈循环。

## 为什么重要

模型本身主要接收输入并生成输出；它不会天然维护持久状态、运行代码、安装依赖、访问实时知识或验证工作结果。这些能力需要由 harness 提供，否则“智能”无法变成可靠工作。

## 来源支持的要点

- LangChain Anatomy 文章从模型视角列出模型 out of the box 做不到的事情：durable state、code execution、realtime knowledge、environment setup。
- 文章把 harness engineering 描述为把“想要的 agent 行为”转化为“对应 harness feature”的过程。
- 行为到组件的映射包括：真实数据持久工作 → filesystem + git；写/执行代码 → bash + code execution；安全执行 → sandbox + tooling；长上下文稳定 → compaction + tool offloading + skills；长时程完成 → Ralph Loop + planning + verification。
- Michael Bolin 访谈从 Codex 角度把 harness 具体化为 agent loop、tool execution、sandbox policy 和 small tool surface。
- Claude Code dynamic workflows 来源把 harness 扩展到按任务临时生成：Claude 可写 JavaScript workflow 来调度子智能体、模型选择、worktree 隔离和验证流程。

## 相关概念

- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Agent Loop|Agent Loop]]
- [[wiki/concepts/Filesystem as Harness Primitive|Filesystem as Harness Primitive]]
- [[wiki/concepts/Bash and Code Execution|Bash and Code Execution]]
- [[wiki/concepts/Sandbox and Tool Orchestration|Sandbox and Tool Orchestration]]
- [[wiki/concepts/Context Engineering for Coding Agents|Context Engineering for Coding Agents]]
- [[wiki/concepts/Load-bearing Harness Components|Load-bearing Harness Components]]
- [[wiki/concepts/Dynamic Workflows|Dynamic Workflows]]

## 开放问题

- “Agent = Model + Harness” 足够简洁，但具体讨论时如何避免把所有东西都塞进 harness？
- Agent harness 的最小可行组件集是什么？
- 产品内置 harness、团队 operating harness 和用户侧 outer harness 应如何分层？
- dynamic workflow 是产品内置 harness 的扩展能力，还是用户侧 outer harness 的可编程表达？
