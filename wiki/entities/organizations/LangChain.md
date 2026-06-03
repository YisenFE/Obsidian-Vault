---
type: organization
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering]]"
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
tags:
  - llm-wiki/entity/organization
  - langchain
---
# LangChain

## 在本 wiki 中的角色

LangChain 是 [[wiki/entities/products/Deep Agents|Deep Agents]] 与 [[wiki/entities/products/LangSmith|LangSmith]] 背后的组织，也是 [[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering|Improving Deep Agents with harness engineering]] 的发布方。

## 来源支持的要点

- LangChain 使用 LangSmith traces 大规模理解 deepagents-cli 的失败模式。
- 来源报告在固定 GPT-5.2-Codex 的情况下，仅通过 harness 改动提升 Terminal Bench 2.0 表现。
- LangChain 计划发布 trace analyzer skill，并共享 trace 数据集。

- LangChain 在 [[wiki/sources/2026-05-28 The Anatomy of an Agent Harness|The Anatomy of an Agent Harness]] 中给出更通用的 Agent = Model + Harness 框架，覆盖 filesystem、bash、sandbox、context management、long-horizon execution 与 model-harness training loop。

## 相关页面

- [[wiki/entities/products/LangSmith|LangSmith]]
- [[wiki/entities/products/Deep Agents|Deep Agents]]
- [[wiki/entities/products/Terminal Bench|Terminal Bench]]
