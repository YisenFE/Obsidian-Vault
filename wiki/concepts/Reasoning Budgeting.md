---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering]]"
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
tags:
  - llm-wiki/concept
  - reasoning
  - harness-engineering
  - latency
---
# Reasoning Budgeting

## 定义

推理预算分配（Reasoning Budgeting）是在 agent run 的不同阶段分配不同推理强度、模型或计算预算的 harness 策略，以平衡质量、时间、token 成本和超时风险。

## 为什么重要

对长时程 agent 来说，最大推理预算并不总是最好。计划和最终验证通常需要更深推理；中间实现阶段可能更受时间/成本约束。错误的推理预算会导致超时或低效。

## 来源支持的要点

- LangChain 在 Terminal Bench 中使用 `gpt-5.2-codex` 的 low/medium/high/xhigh reasoning modes。
- 他们发现规划阶段和最终验证更适合高推理，中间 build/iterate 阶段可以较低预算。
- 采用 xhigh-high-xhigh “reasoning sandwich”：前 25% 计划理解用 xhigh，中间 50% build iterate 用 high，最后 25% final verification 用 xhigh。
- xhigh-only 得分 53.9%，差于 high 的 63.6%，原因是 strict timeout 下更多推理消耗时间/token。
- Anthropic harness design 来源也强调模型能力变化会移动 harness 组件的承重性；reasoning budgeting 同样应随模型和任务重测。

## 相关概念

- [[wiki/concepts/Load-bearing Harness Components|Load-bearing Harness Components]]
- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Build-Verify Loop|Build-Verify Loop]]
- [[wiki/concepts/Context Reset vs Compaction|Context Reset vs Compaction]]

## 开放问题

- 如何动态判断当前阶段需要多少 reasoning？
- 多模型 harness 中，何时用大模型规划、小模型实现？
- Reasoning budget 的收益应如何和 latency/cost 一起度量？
