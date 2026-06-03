---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
aliases:
  - Bash + Code Execution
  - Code execution as general purpose tool
sources:
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
tags:
  - llm-wiki/concept
  - tools
  - code-execution
  - harness-engineering
---
# Bash and Code Execution

## 定义

Bash 与代码执行（Bash and Code Execution）是一种通用工具型 harness 设计：给 agent 终端/脚本执行能力，让模型可以临时编写代码、运行命令、构造小工具，而不是要求用户预先为每种动作定义专用 tool。

## 为什么重要

许多任务的行动空间无法提前枚举。Bash/code execution 相当于给模型一台可控计算机，使它能从现有命令、语言运行时和脚本组合中自行探索解法；但这种能力必须由 sandbox、权限和默认工具配置约束。

## 来源支持的要点

- LangChain Anatomy 文章把 ReAct loop 中的 bash + code execution 视为给模型 general-purpose tool，使其不被固定工具集限制。
- 文章说模型可以 on the fly 设计自己的工具，code execution 已成为 autonomous problem solving 的默认通用策略之一。
- Bolin 访谈中 Codex 也倾向 small/tight harness：不给显式 read-file tool，而是给 terminal，让模型用系统工具完成读写探索。

## 相关概念

- [[wiki/concepts/Small Powerful Tool Surface|Small Powerful Tool Surface]]
- [[wiki/concepts/Sandbox and Tool Orchestration|Sandbox and Tool Orchestration]]
- [[wiki/concepts/Agent Loop|Agent Loop]]
- [[wiki/concepts/Filesystem as Harness Primitive|Filesystem as Harness Primitive]]

## 开放问题

- 哪些场景适合 bash/code execution，哪些场景必须使用更受限的专用工具？
- 模型临时生成工具的行为如何审计和复用？
- 通用终端能力会不会提高 prompt injection 或误操作风险？
