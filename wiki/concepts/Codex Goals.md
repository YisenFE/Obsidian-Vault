---
type: concept
status: draft
created: 2026-06-01
updated: 2026-06-01
aliases:
  - Goals in Codex
  - Codex Goal
sources:
  - "[[wiki/sources/2026-06-01 Using Goals in Codex]]"
tags:
  - llm-wiki/concept
  - codex
  - goals
  - harness-engineering
---
# Codex Goals

## 定义

Codex Goals（Codex 目标）是附着在 Codex thread 上的持久目标状态，用来把一次性 prompt 转成围绕明确 outcome 的 evidence-checked continuation loop。Goal 不是让 Codex 无限后台运行，而是让用户定义完成契约，由证据决定是否完成。

## 为什么重要

很多 coding/research 任务不是“下一步做什么”清楚，而是“最终要达到什么”清楚，中间路径需要根据测试、benchmark、日志或研究材料不断调整。Goal 让目标跨 turn 保持可见，减少用户反复说“继续、再试、跑 benchmark、别停到真正完成”的操作成本。

## 来源支持的要点

- 来源把 Goal 定义为 persistent objective：包含什么应为真、如何验证、哪些约束必须保持。
- 适用任务包括性能优化、flaky test 调查、依赖迁移、bug hunt、多步 refactor、benchmark tuning、研究型 evidence-backed audit。
- 命令表面包括 `/goal <outcome>`、`/goal`、`/goal pause`、`/goal resume`、`/goal clear`。
- 来源称 Goals 从 Codex 0.128.0 开始可用。
- Goal active 后，Codex 能在 thread idle 且 within budget 时从最新证据继续。

## 相关概念

- [[wiki/concepts/Goal Completion Contract|Goal Completion Contract]]
- [[wiki/concepts/Goal Lifecycle and Continuation Gates|Goal Lifecycle and Continuation Gates]]
- [[wiki/concepts/Evidence-Based Completion|Evidence-Based Completion]]
- [[wiki/concepts/Agent Loop|Agent Loop]]
- [[wiki/entities/products/Codex|Codex]]

## 开放问题

- 团队应该为哪些任务默认启用 Goal？
- Goal progress accounting 应如何外化到文件、PR、日志或报告？
- Goal 与 agent memory / progress file / NLAH artifact contract 如何组合？
