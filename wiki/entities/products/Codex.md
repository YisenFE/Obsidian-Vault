---
type: product
status: draft
created: 2026-05-28
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 工程技术：在智能体优先的世界中利用 Codex]]"
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
  - "[[wiki/sources/2026-06-01 Using Goals in Codex]]"
tags:
  - llm-wiki/entity/product
  - codex
---
# Codex

## 在本 wiki 中的角色

Codex 是 OpenAI 的 coding agent/product，在 Codex-first engineering 来源中承担核心执行者角色。

## 来源支持的要点

- 来源描述的实验中，Codex 生成代码、测试、CI、文档、可观测性和内部工具。
- Codex 使用 `gh`、本地脚本和仓库内 skills 等标准开发工具收集上下文并推进 PR。
- Codex 可通过 [[wiki/entities/products/Chrome DevTools MCP|Chrome DevTools MCP]] 和可观测性 API 获得 UI/运行时访问能力，形成 reproduce-fix-verify 循环。
- 来源称 Codex 能做长时间运行，有时单个任务超过六小时。

- Michael Bolin 访谈把 Codex 进一步描述为 open-source coding agent，其 harness 负责 agent loop、tool orchestration 与 sandboxing。
- Codex 的工具设计倾向少量强工具：不给专门 read-file tool，而让 agent 使用 terminal 和系统命令探索代码。
- Codex App 则提供 mission control 式界面，让开发者管理多个并行 agent conversations。

- LangChain Anatomy 文章把 Codex 与 Claude Code 一起作为“模型与 harness 一起后训练”的 agent product 例子，并用 Codex-5.3 prompting guide 中 apply_patch tool logic 讨论 tool-protocol overfitting。

- Using Goals in Codex 来源把 Codex 的 Goal 功能描述为 thread-scoped completion contract：Codex 可围绕持久目标跨 turn 继续，但 completion 必须对照测试、日志、benchmark、artifact 或研究证据。
- 该来源说明 Goal 不属于 global memory 或 project instructions，而是当前 thread 的 durable objective state。

- [[wiki/concepts/Codex Goals|Codex Goals]]
- [[wiki/concepts/Goal Completion Contract|Goal Completion Contract]]

## 相关概念

- [[wiki/concepts/Agent Loop|Agent Loop]]
- [[wiki/concepts/Sandbox and Tool Orchestration|Sandbox and Tool Orchestration]]
- [[wiki/concepts/Small Powerful Tool Surface|Small Powerful Tool Surface]]

- [[wiki/concepts/Codex-first Development|Codex-first Development]]
- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Agent-readable Codebase|Agent-readable Codebase]]
