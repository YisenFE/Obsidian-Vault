---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering]]"
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
tags:
  - llm-wiki/concept
  - middleware
  - harness-engineering
  - agent-loop
---
# Middleware Hooks

## 定义

中间件/调用拦截点（Middleware Hooks）是围绕模型调用和工具调用的可编程拦截/增强点，用来注入上下文、检查状态、提示下一步、限制循环、记录指标或改变 agent loop 的执行流。

## 为什么重要

仅靠 system prompt 往往不足以稳定改变 agent 行为。Middleware 可以在关键时刻确定性地注入上下文或反馈，例如启动时提供环境地图、退出前要求验证、重复编辑时提示重新考虑方案。

## 来源支持的要点

- LangChain 将 middleware 定义为围绕 model 和 tool calls 的 hooks，是其重点优化的三类 harness knobs 之一。
- `PreCompletionChecklistMiddleware` 在 agent 退出前提醒它对 task spec 做 verification pass。
- `LocalContextMiddleware` 在 agent 启动时映射 cwd、父/子目录并寻找可用工具。
- `LoopDetectionMiddleware` 通过 tool call hooks 统计每个文件编辑次数，在可能的 doom loop 中注入“重新考虑方案”的上下文。
- Middleware 是一种短期围绕当前模型缺陷的工程 guardrail，未来可能随模型能力提高而失去必要性。

- Claude Code shorthand 来源展示了产品级 hooks 的用户配置版本：PreToolUse、PostToolUse、UserPromptSubmit、Stop、PreCompact、Notification。
- 这些 hooks 可以承担 LangChain middleware 相似职责：在工具调用前后注入提醒、格式化、类型检查、日志扫描、push 前 review 和 stop 前审计。
- 与纯 prompt 相比，hooks 更接近可执行 guardrails，但也需要测试，避免误伤不同项目。

## 相关概念

- [[wiki/concepts/Build-Verify Loop|Build-Verify Loop]]
- [[wiki/concepts/Local Context Injection|Local Context Injection]]
- [[wiki/concepts/Load-bearing Harness Components|Load-bearing Harness Components]]
- [[wiki/concepts/Feedback Sensors|Feedback Sensors]]

- [[wiki/concepts/Claude Code Hooks|Claude Code Hooks]]

## 开放问题

- Middleware 应保持多轻量，避免把 agent loop 变得难以解释？
- 哪些 prompt-level 指令应该升级为 middleware？
- Middleware 本身如何测试和回归评估？
