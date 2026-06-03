---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
aliases:
  - Ralph Loop
sources:
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
tags:
  - llm-wiki/concept
  - long-running-agents
  - harness-pattern
---
# Ralph Loop

## 定义

Ralph Loop（Ralph 循环）是一种长时程 agent harness 模式：当模型尝试退出或声明完成时，harness hook 拦截退出，在干净上下文窗口中重新注入原始目标，并让 agent 读取文件系统中的既有状态继续工作。

## 为什么重要

长任务中 agent 常见问题是 early stopping（过早停止）和跨上下文不连贯。Ralph Loop 把“继续做直到满足完成目标”变成 harness 逻辑，而不完全依赖模型一次性自觉坚持。

## 来源支持的要点

- LangChain Anatomy 文章把 Ralph Loop 放在 long horizon autonomous execution 组件中。
- 该模式依赖文件系统：每轮用 clean context 开始，但通过上一轮写下的状态继续推进。
- 它与 planning、self-verification、git/history 组合，目标是让 agent 在多个上下文窗口中持续工作。

## 相关概念

- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]]
- [[wiki/concepts/Filesystem as Harness Primitive|Filesystem as Harness Primitive]]
- [[wiki/concepts/Context Reset vs Compaction|Context Reset vs Compaction]]
- [[wiki/concepts/Self-verification|Self-verification]]
- [[wiki/concepts/Artifact Contract|Artifact Contract]]

## 开放问题

- Ralph Loop 的停止条件应如何避免无限循环或过度修改？
- 它应依赖原始 prompt、artifact contract，还是独立 evaluator 的验收？
- 与 Anthropic context reset / NLAH handoff 相比，Ralph Loop 更适合哪些任务？
