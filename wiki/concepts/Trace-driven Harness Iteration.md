---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering]]"
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
tags:
  - llm-wiki/concept
  - harness-engineering
  - tracing
  - evaluation
---
# Trace-driven Harness Iteration

## 定义

基于执行轨迹的工作支架迭代（Trace-driven Harness Iteration）是用 agent traces 作为外部反馈信号来改进 harness 的方法：先收集大量 agent run 的输入、输出、工具调用、错误和成本指标，再分析失败模式，最后针对性修改 prompt、tools、middleware 或流程。

## 为什么重要

模型内部难以解释，但 agent 在文本和工具空间中的行为是可观察的。Trace 让 harness 工程从“凭直觉改提示词”转向“基于失败模式改系统”，也让改动可以和 benchmark/指标形成闭环。

## 来源支持的要点

- LangChain 将每个 agent action 存到 [[wiki/entities/products/LangSmith|LangSmith]]，包括 latency、token counts 和 costs。
- Trace Analyzer Skill 的流程是：fetch experiment traces，spawn parallel error analysis agents，main agent synthesize findings + suggestions，aggregate feedback and make targeted changes。
- 文章把这类做法类比为 boosting：重点关注上一轮 mistakes。
- 人类在改 harness 的第三步仍有价值，用于验证和讨论建议，避免过拟合特定 task。
- LangChain 公开了 traces dataset，作为社区研究材料。

- LangChain Anatomy 来源把“agents analyze their own traces to identify and fix harness-level failure modes”列为未来方向，说明 trace-driven iteration 可能从人类/外部分析 agent 扩展为 agent 自诊断 harness。
- 这与既有 LangChain Deep Agents 来源中的 Trace Analyzer Skill 形成连续线索：先让分析 agent 聚合失败，再进一步让 agent 主动改进 harness-level issues。

## 相关概念

- [[wiki/concepts/Feedback Sensors|Feedback Sensors]]
- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Load-bearing Harness Components|Load-bearing Harness Components]]
- [[wiki/entities/products/LangSmith|LangSmith]]

- [[wiki/concepts/Model-Harness Co-evolution|Model-Harness Co-evolution]]

## 开放问题

- Trace analyzer 如何区分真实通用失败模式和 benchmark overfit？
- Trace-derived harness changes 如何做 A/B 或回归评估？
- 团队日常开发中的 traces 是否足够结构化，能支持同样的分析？
