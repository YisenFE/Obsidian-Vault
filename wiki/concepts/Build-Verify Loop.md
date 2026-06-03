---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering]]"
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
tags:
  - llm-wiki/concept
  - verification
  - testing
  - harness-engineering
---
# Build-Verify Loop

## 定义

构建-验证循环（Build-Verify Loop）是让 coding agent 在一次 run 内反复执行“规划/发现 → 构建 → 验证 → 修复”的循环，直到输出满足原始任务 spec，而不是在写完第一版后凭代码阅读自信结束。

## 为什么重要

Agent 常见失败模式是：写出解决方案、重读自己的代码、觉得没问题就停止。对 autonomous coding 来说，测试和验证既是 correctness check，也是 agent 可以 hill-climb 的反馈信号。

## 来源支持的要点

- LangChain 发现最常见失败模式是 agent 写完后只读代码并停止，没有充分测试。
- 他们在 system prompt 中加入 Planning & Discovery、Build、Verify、Fix 四步。
- Verify 阶段要求运行测试、读完整输出，并对照任务 spec，而不是对照 agent 自己写的代码。
- `PreCompletionChecklistMiddleware` 会在 agent 退出前注入提醒，让它做一轮 verification pass。
- Anthropic long-running agents 来源也强调只有经过端到端测试后才能把 feature 标为 passing。

## 相关概念

- [[wiki/concepts/Self-verification|Self-verification]]
- [[wiki/concepts/Feedback Sensors|Feedback Sensors]]
- [[wiki/concepts/Middleware Hooks|Middleware Hooks]]
- [[wiki/concepts/Behaviour Harness|Behaviour Harness]]

## 开放问题

- 如何避免 agent 写低质量测试来满足自己的验证循环？
- Build-verify 循环何时应该停止，如何避免无限 retry？
- 哪些任务没有可自动运行测试时，应该用什么替代 verification signal？
