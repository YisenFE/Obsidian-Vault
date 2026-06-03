---
type: person
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering]]"
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
tags:
  - llm-wiki/entity/person
---
# Vivek Trivedy

## 在本 wiki 中的角色

[[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering|Improving Deep Agents with harness engineering]] 与 [[wiki/sources/2026-05-28 The Anatomy of an Agent Harness|The Anatomy of an Agent Harness]] 的作者。前者讨论如何通过 harness 改动提升 deepagents-cli 在 Terminal Bench 上的表现，后者从模型能力边界倒推 agent harness 的核心 primitive。

## 来源支持的要点

- 介绍 LangChain 使用 LangSmith traces、自验证、上下文注入、循环检测和推理预算分配来迭代 harness。
- 报告在固定模型下，Terminal Bench 2.0 分数从 52.8 提升到 66.5。
- 提出 Agent = Model + Harness，并把 filesystem、bash/code execution、sandbox、context rot management、Ralph Loop 和 model-harness co-evolution 作为关键 anatomy。

## 相关页面

- [[wiki/entities/organizations/LangChain|LangChain]]
- [[wiki/entities/products/Deep Agents|Deep Agents]]
- [[wiki/concepts/Trace-driven Harness Iteration|Trace-driven Harness Iteration]]
