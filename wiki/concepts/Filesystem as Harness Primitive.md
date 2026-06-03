---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
aliases:
  - Filesystem primitive
  - Agent filesystem
sources:
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
tags:
  - llm-wiki/concept
  - filesystem
  - state-management
  - harness-engineering
---
# Filesystem as Harness Primitive

## 定义

文件系统作为工作支架原语（Filesystem as Harness Primitive）是指把可读写文件、目录和 git workspace 作为 agent 的持久工作面，让智能体能读取真实数据、保存中间结果、卸载上下文、跨 session 交接，并与人类或其他 agent 协作。

## 为什么重要

Context window 是短暂且有限的；文件系统是持久、可审计、可增量读取的状态层。它把 agent 的工作从“一次对话里的文本”转成“可恢复的项目状态”。

## 来源支持的要点

- LangChain Anatomy 文章称 filesystem 可能是最基础的 harness primitive，因为它支持 workspace、incremental work、context offload、persistent state 和 collaboration surface。
- Git 给文件系统加上版本化：agent 可以追踪进展、回滚错误、分支实验，新 agent 可以通过 history 快速理解项目。
- Anthropic 长时程来源使用 progress file、feature list、git history 解决跨 session 失忆。
- NLAH 论文的 file-backed state ablation 对多个 benchmark 有正向证据，支持“状态落文件”比只靠上下文更稳。

## 相关概念

- [[wiki/concepts/File-backed State|File-backed State]]
- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]]
- [[wiki/concepts/Repository as System of Record|Repository as System of Record]]
- [[wiki/concepts/Tool Call Offloading|Tool Call Offloading]]
- [[wiki/concepts/Ralph Loop|Ralph Loop]]

## 开放问题

- 哪些 agent 状态应写入文件，哪些只需保留在上下文？
- 文件系统作为协作面时，如何处理并发写入、冲突和 stale state？
- Git history 对新 agent 是足够的交接信号，还是必须配合结构化 progress artifact？
