---
type: product
status: stub
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
tags:
  - llm-wiki/entity/product
  - anthropic
  - model
---
# Claude Sonnet 4.5

## 在本 wiki 中的角色

Claude Sonnet 4.5 是 Anthropic 来源中提到的模型；它在早期长时程 harness 测试中表现出足够明显的 context anxiety，使 context reset 变得重要。

## 来源支持的要点

- Harness design 来源称 Sonnet 4.5 的 context anxiety 让单靠 compaction 不足以获得强长任务表现。
- 这种模型特定行为被用作证据：harness 结构应随模型能力变化重新测试。

## 相关概念

- [[wiki/concepts/Context Reset vs Compaction|Context Reset vs Compaction]]
- [[wiki/concepts/Load-bearing Harness Components|Load-bearing Harness Components]]
