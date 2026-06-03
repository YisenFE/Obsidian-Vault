---
type: concept
status: draft
created: 2026-06-01
updated: 2026-06-01
aliases:
  - Completion contract
  - Goal contract
sources:
  - "[[wiki/sources/2026-06-01 Using Goals in Codex]]"
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
tags:
  - llm-wiki/concept
  - goals
  - completion
  - harness-engineering
---
# Goal Completion Contract

## 定义

Goal Completion Contract（目标完成契约）是把 Codex 目标写成可审计协议：它明确最终状态、验证面、约束、边界、迭代策略和阻塞停止条件。它回答的不是“下一步做什么”，而是“什么时候可以诚实地说完成”。

## 为什么重要

没有完成契约，长任务很容易早停、过度自信、只交付看似合理的 artifact，或者在 blocker 出现后把不确定性包装成成功。完成契约让 Codex 可以自由探索路径，但不能自由改写完成标准。

## 来源支持的要点

- 来源列出强 Goal 的六项要素：outcome、verification surface、constraints、boundaries、iteration policy、blocked stop condition。
- 模板要求写明 desired end state、specific evidence、constraints、allowed inputs/tools/boundaries、between-iteration policy、blocked reporting。
- 性能例子中，p95 < 120ms 是 outcome，checkout benchmark 是 verification surface，correctness suite green 是 constraint。
- 研究例子中，最终 artifact 是报告，并要求区分 confirmed、approximate、blocked、remaining uncertainty。
- NLAH 的 artifact contract/stopping conditions 与该概念同构：二者都把完成绑定到可审计证据。

## 相关概念

- [[wiki/concepts/Codex Goals|Codex Goals]]
- [[wiki/concepts/Artifact Contract|Artifact Contract]]
- [[wiki/concepts/Evidence-Based Completion|Evidence-Based Completion]]
- [[wiki/concepts/Self-verification|Self-verification]]

## 开放问题

- 完成契约应如何模板化，以便团队复用？
- 不同任务类型的 verification surface 如何标准化？
- Blocked stop condition 应由用户、agent，还是团队 policy 给出？
