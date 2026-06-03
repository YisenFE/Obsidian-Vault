---
type: product
status: stub
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
  - "[[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering]]"
tags:
  - llm-wiki/entity/product
  - anthropic
  - model
---
# Claude Opus 4.6

## 在本 wiki 中的角色

Claude Opus 4.6 是 Anthropic 与 LangChain harness 来源都提到的 Anthropic 模型，用来说明模型能力会改变 harness 设计和 benchmark 结果。

## 来源支持的要点

- Anthropic harness design 来源称 Opus 4.6 改善了规划、长时程 agentic task 可靠性、大代码库操作、代码 review/debugging 和长上下文检索。
- 这些提升促使作者移除 sprint construct，并降低 evaluator 频率。
- 在 DAW 实验中，builder 在没有 sprint decomposition 的情况下连贯运行两个多小时，但 QA 仍抓到有意义的功能缺口。
- LangChain 来源报告 Claude Opus 4.6 在早期 harness 版本上得 59.6%，同时提醒他们没有对 Claude 运行同样的 improvement loop。

## 相关概念

- [[wiki/concepts/Load-bearing Harness Components|Load-bearing Harness Components]]
- [[wiki/concepts/Reasoning Budgeting|Reasoning Budgeting]]
- [[wiki/concepts/Planner-Generator-Evaluator Harness|Planner-Generator-Evaluator Harness]]
