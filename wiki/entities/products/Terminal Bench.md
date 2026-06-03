---
type: product
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
  - "[[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering]]"
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
tags:
  - llm-wiki/entity/product
  - benchmark
  - coding-agent
---
# Terminal Bench

## 在本 wiki 中的角色

Terminal Bench 是 LangChain 用来衡量 harness changes 的 agentic coding benchmark，出现在 [[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering|Improving Deep Agents with harness engineering]] 中。

## 来源支持的要点

- 来源使用 Terminal Bench 2.0，其中包含 89 个跨机器学习、debugging、生物等领域的任务。
- LangChain 报告 Deep Agents 从 Terminal Bench 2.0 排行榜 Top 30 外提升到 Top 5 左右。
- 该 benchmark 有严格 timeout，因此 time-budgeting 和 reasoning-budget 选择尤其重要。
- NLAH 论文把 Terminal-Bench 2.0 作为 terminal-use benchmark，用 MHTBA 对比 code、prompt 与 NLAH/IHR execution；报告 NLAH 53.9、prompt 57.3、code 36.0。

- LangChain Anatomy 文章再次引用 Terminal Bench 2.0 作为“最佳 harness 不一定是模型后训练 harness”的证据场景：同一模型在不同 harness 下表现可显著不同。

## 相关概念

- [[wiki/concepts/Reasoning Budgeting|Reasoning Budgeting]]
- [[wiki/concepts/Trace-driven Harness Iteration|Trace-driven Harness Iteration]]
