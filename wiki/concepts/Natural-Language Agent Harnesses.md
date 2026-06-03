---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
aliases:
  - NLAH
  - Natural-Language Agent Harness
sources:
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
tags:
  - llm-wiki/concept
  - harness-engineering
  - natural-language-harness
---
# Natural-Language Agent Harnesses

## 定义

自然语言智能体工作支架（Natural-Language Agent Harnesses，NLAHs）是用可编辑自然语言文档表达的 run-level harness policy：它描述一次 agent run 中的角色、状态、交接、验证 gate、产物契约、恢复策略和停止条件，并由 [[wiki/concepts/Intelligent Harness Runtime|Intelligent Harness Runtime]] 解释执行。

## 为什么重要

NLAH 把 harness 从 controller code 中抽出来，变成可读、可比较、可迁移、可 ablate 的对象。它不是替代所有代码，而是把高层 policy 暴露出来，让研究者和工程师能审计“到底是哪种 harness policy 造成差异”。

## 来源支持的要点

- 论文把 NLAH 定义为 editable documents，用来描述 run-level harness policy。
- RQ1 显示 NLAH+IHR 在 coding、terminal-use、computer-use 三类 benchmark 中达到与 code/prompt realization 同量级的 task outcomes。
- NLAH 的静态 policy 更短：Live-SWE 从 60.1k token code materials 降到 2.9k-token NLAH；MHTBA 从 10.5k 降到 0.8k；OSWorld/SeeAct 从 47.5k 降到 1.4k。
- NLAH 最适合表达 goals、evidence、gates、roles、retry rules、validation strategy 和 state handoff，而不是精确 parser、sandbox 或 deterministic validator。
- 论文把未来方向称为 harness representation science：检索、组合、变异和优化 NLAH modules。

## 相关概念

- [[wiki/concepts/Intelligent Harness Runtime|Intelligent Harness Runtime]]
- [[wiki/concepts/Harness Policy Layer|Harness Policy Layer]]
- [[wiki/concepts/Artifact Contract|Artifact Contract]]
- [[wiki/concepts/Harness Module Ablation|Harness Module Ablation]]
- [[wiki/concepts/Harness Engineering|Harness Engineering]]

## 开放问题

- NLAH 与 `AGENTS.md`、skills、prompt template、workflow DSL 的边界如何划分？
- NLAH 何时需要机器可验证 schema，而何时保持自然语言自由度更有价值？
- NLAH 是否会把 prompt injection 或危险 workflow 的传播变得更容易？
