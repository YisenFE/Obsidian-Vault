---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
  - "[[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering]]"
tags:
  - llm-wiki/concept
  - evaluation
  - harness-engineering
---
# Harness Module Ablation

## 定义

工作支架模块消融（Harness Module Ablation）是在共享 runtime 或相同任务条件下，逐个增删 harness module，观察 performance、agent calls、tool calls、handoff、artifact compliance 等指标变化，以判断哪些模块真正承重。

## 为什么重要

复杂 harness 容易堆叠组件，但更多流程不一定更好。把 modules 显式化后，可以从“整个系统 A 比系统 B 强”进一步追问“哪个 policy choice 或 module 造成差异”。

## 来源支持的要点

- NLAH 论文 RQ3 使用同一 IHR 对 explicit NLAH modules 做 ablation。
- File-backed state、self-evolution、evidence-backed answering 整体正向，因为它们缩短了从中间工作到可审计证据和最终验收的路径。
- Multi-candidate search 明显增加 agent calls，但在 SWE 上降低 performance；context compression 在 SWE 和 OSWorld 都有负面结果。
- LangChain 来源也体现相同思想：固定模型后分别调 prompt、middleware、reasoning schedule，从而判断哪些 harness knobs 有用。

## 相关概念

- [[wiki/concepts/Load-bearing Harness Components|Load-bearing Harness Components]]
- [[wiki/concepts/Trace-driven Harness Iteration|Trace-driven Harness Iteration]]
- [[wiki/concepts/Harness Policy Layer|Harness Policy Layer]]
- [[wiki/concepts/Natural-Language Agent Harnesses|Natural-Language Agent Harnesses]]

## 开放问题

- Harness module ablation 应该优先看 task performance，还是同时约束成本、延迟和安全风险？
- 模块间存在交互效应时，如何避免单模块消融误判？
- 如何把 ablation 结果转化为可复用 harness template？
