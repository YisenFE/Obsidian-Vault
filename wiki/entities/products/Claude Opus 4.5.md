---
type: product
status: stub
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
tags:
  - llm-wiki/entity/product
  - anthropic
  - model
---
# Claude Opus 4.5

## 在本 wiki 中的角色

Claude Opus 4.5 是 [[wiki/sources/2026-05-28 Harness design for long-running application development|Harness design for long-running application development]] 中第一版 planner/generator/evaluator full-stack harness 实验使用的 Anthropic 模型。

## 来源支持的要点

- 作者使用 Opus 4.5，是因为实验开始时它是 Anthropic 最强 coding model。
- 与早期 harness 中的 [[wiki/entities/products/Claude Sonnet 4.5|Claude Sonnet 4.5]] 不同，Opus 4.5 基本移除了 context anxiety，因此新 harness 可以放弃 context resets，以一个连续 session 和自动 compaction 运行。

## 相关概念

- [[wiki/concepts/Context Reset vs Compaction|Context Reset vs Compaction]]
- [[wiki/concepts/Load-bearing Harness Components|Load-bearing Harness Components]]
