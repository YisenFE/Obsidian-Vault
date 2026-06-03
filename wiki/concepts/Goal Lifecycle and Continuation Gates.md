---
type: concept
status: draft
created: 2026-06-01
updated: 2026-06-01
aliases:
  - Goal lifecycle
  - Continuation gates
sources:
  - "[[wiki/sources/2026-06-01 Using Goals in Codex]]"
tags:
  - llm-wiki/concept
  - goals
  - agent-loop
  - lifecycle
---
# Goal Lifecycle and Continuation Gates

## 定义

Goal Lifecycle and Continuation Gates（目标生命周期与继续门控）描述 Codex Goal 何时 active、paused、complete、budget-limited 或 cleared，以及 Codex 何时允许自动继续。Continuation gate 是防止 Goal 变成无限循环或越权后台工作的安全边界。

## 为什么重要

持久目标如果没有门控，就会变成不可控后台 agent。Codex Goals 的设计重点是“可以继续，但只在安全边界继续”：thread 必须 idle、没有 queued user input、没有其他 pending work、Goal active、预算未耗尽。

## 来源支持的要点

- Goal lifecycle 包括 active、paused、complete、budget-limited、cleared 等状态。
- Continuation 是 event-driven，不是简单 loop；Codex 在 turn 完成和 thread idle 等 safe boundary 检查。
- Plan-only work 不触发 continuation；interruptions 会 pause；resume 可恢复 objective。
- 如果 continuation turn 没有 tool call，下一次自动 continuation 会被抑制，避免 spin。
- Budget hit 时应停止实质工作，报告进展、blockers 和下一步；budget-limited 不等于完成。
- Model 可在证据支持时 mark complete；pause/resume/clear/budget-limited transitions 由用户或系统控制。

## 相关概念

- [[wiki/concepts/Codex Goals|Codex Goals]]
- [[wiki/concepts/Agent Loop|Agent Loop]]
- [[wiki/concepts/Goal Completion Contract|Goal Completion Contract]]
- [[wiki/concepts/Sandbox and Tool Orchestration|Sandbox and Tool Orchestration]]

## 开放问题

- No-tool-call continuation suppression 是否足以防止低价值循环？
- Budget 应该以什么单位设置和展示？
- Goal pause/resume 与人为 review gate 如何结合？
