---
type: product
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
tags:
  - llm-wiki/entity/product
  - anthropic
  - agent-sdk
---
# Claude Agent SDK

## 在本 wiki 中的角色

Claude Agent SDK 是 Anthropic 来源中的 agent harness/runtime 基座，用于长时程 coding agents、前端 evaluator 循环，以及 planner/generator/evaluator full-stack 应用构建。

## 来源支持的要点

- 早期文章把 Claude Agent SDK 描述为用于 coding 和其他 tool-using tasks 的通用 agent harness。
- SDK 包含 compaction 等 context management 能力，但 Anthropic 认为 compaction alone 并不总能支撑长时程工作。
- 早期 harness 在 SDK 上叠加 initializer/coding-agent prompts、progress artifacts、git history、feature lists 与 browser automation。
- 后续文章在 SDK 上构建 generator/evaluator design loops 和 planner/generator/evaluator application harnesses，并用 [[wiki/entities/products/Playwright MCP|Playwright MCP]] 作为 evaluator 工具。
- 在 Opus 4.5/4.6 实验中，当不再需要 context resets 时，SDK automatic compaction 处理了上下文增长。

## 相关概念

- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]]
- [[wiki/concepts/Planner-Generator-Evaluator Harness|Planner-Generator-Evaluator Harness]]
- [[wiki/concepts/Self-verification|Self-verification]]
