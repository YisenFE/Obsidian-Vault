---
type: concept
status: draft
created: 2026-06-01
updated: 2026-06-01
aliases:
  - Scoped subagents
  - Subagent permissions
sources:
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
tags:
  - llm-wiki/concept
  - subagents
  - claude-code
  - permissions
---
# Subagent Scoping

## 定义

Subagent Scoping（子智能体范围限定）是把主 agent 可委派的任务拆给有限职责、有限工具、有限 MCP 和有限权限的 subagents。它强调 subagent 的角色、可见上下文和工具边界要与任务匹配。

## 为什么重要

Subagents 能释放主 agent 上下文、并行处理专门任务，但如果范围太宽，就会复制主 agent 的混乱。通过 planner、architect、code-reviewer、security-reviewer、e2e-runner、refactor-cleaner 等角色化拆分，可以把 delegation 变成结构化工作流。

## 来源支持的要点

- Claude Code shorthand 来源把 subagents 定义为 orchestrator 可委派的有限范围进程，可前台/后台运行，释放主 agent context。
- 来源建议为每个 subagent 配置 allowed tools、MCPs 和 permissions。
- Subagents 与 skills 可以组合：subagent 可执行某个 skill 子集，并自主完成委派任务。
- Anthropic planner/generator/evaluator 来源也支持角色分工：planner 定义范围，generator 实现，evaluator 外部 QA。

## 相关概念

- [[wiki/concepts/Planner-Generator-Evaluator Harness|Planner-Generator-Evaluator Harness]]
- [[wiki/concepts/External Evaluator Agent|External Evaluator Agent]]
- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]]
- [[wiki/concepts/Skills as Progressive Disclosure|Skills as Progressive Disclosure]]

## 开放问题

- Subagent 权限应如何默认最小化？
- 什么时候用 skill 就够，什么时候应拆成 subagent？
- 多 subagent 的输出如何做 provenance、冲突合并和质量验收？
