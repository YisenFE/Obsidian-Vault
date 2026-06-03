---
type: product
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering]]"
tags:
  - llm-wiki/entity/product
  - langchain
  - observability
  - tracing
---
# LangSmith

## 在本 wiki 中的角色

LangSmith 是 LangChain 的 tracing/observability product，在 [[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering|Improving Deep Agents with harness engineering]] 中作为 trace store 和分析基座。

## 来源支持的要点

- 实验中的每个 agent action 都存入 LangSmith。
- LangSmith traces 包含 latency、token counts、costs 等指标。
- Trace Analyzer Skill 先从 LangSmith 抓取实验 traces，再派发并行 error-analysis agents。

## 相关概念

- [[wiki/concepts/Trace-driven Harness Iteration|Trace-driven Harness Iteration]]
- [[wiki/concepts/Feedback Sensors|Feedback Sensors]]
