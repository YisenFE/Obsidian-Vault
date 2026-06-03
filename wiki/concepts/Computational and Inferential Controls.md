---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Harness engineering for coding agent users]]"
tags:
  - llm-wiki/concept
  - harness-engineering
  - controls
---
# Computational and Inferential Controls

## 定义

计算化与推断式控制（Computational and Inferential Controls）是 Böckeler 对 guides/sensors 的执行类型区分：computational controls 由传统程序/CPU 执行，确定性、快速、可频繁运行；inferential controls 由 LLM/语义判断执行，更慢、更贵、更不确定，但能处理自然语言、语义和品味判断。

## 为什么重要

Harness 设计不能把所有控制都当作同一种东西。能用确定性工具表达的约束通常应该优先计算化；需要语义判断的部分才交给 inferential sensors 或 review agents，并根据成本/风险放在合适生命周期位置。

## 来源支持的要点

- Computational examples: tests、linters、type checkers、structural analysis、codemods、language servers、static analysis。
- Inferential examples: AGENTS.md/skills 中的 coding conventions、AI code review、LLM-as-judge、review instructions。
- Computational sensors 足够便宜快速，可以随 agent 在每次 change 上运行。
- Inferential controls 虽非确定且昂贵，但可以提供丰富指导和语义判断，尤其在模型足够适配任务时增加信任。
- Böckeler 的生命周期图将 inferential/computational controls 分布在 initial generation、self-correction loop、human review 和 pipeline 中。

## 相关概念

- [[wiki/concepts/Feedforward Guides|Feedforward Guides]]
- [[wiki/concepts/Feedback Sensors|Feedback Sensors]]
- [[wiki/concepts/Mechanized Invariants|Mechanized Invariants]]
- [[wiki/concepts/External Evaluator Agent|External Evaluator Agent]]

## 开放问题

- 如何把一个反复出现的 inferential judgment 逐步转成 computational control？
- Inferential sensors 的不确定性如何测试、版本化和回归检测？
- 哪些语义判断永远难以计算化？
