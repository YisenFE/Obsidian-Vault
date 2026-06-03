---
type: concept
status: draft
created: 2026-06-03
updated: 2026-06-03
aliases:
  - Agentic laziness
  - Self-preferential bias
  - Goal drift
sources:
  - "[[wiki/sources/2026-06-03 A harness for every task dynamic workflows in Claude Code]]"
tags:
  - llm-wiki/concept
  - long-running-agents
  - failure-modes
  - verification
---
# Long-running Agent Failure Modes

## 定义

长时程智能体失败模式（Long-running Agent Failure Modes）是智能体在复杂、多轮、长上下文或多步骤任务中更容易出现的系统性偏差。Claude Code dynamic workflows 来源重点列出三类：agentic laziness（智能体懒惰）、self-preferential bias（自我偏好偏差）和 goal drift（目标漂移）。

## 为什么重要

这些失败不是单个 prompt 写得不好，而是单上下文 agent 承担计划、执行、验证和记忆时的结构性风险。Dynamic workflows、external evaluator、file-backed state、artifact contract 和 evidence-based completion 都是在把这些风险拆开处理。

## 来源支持的要点

- **Agentic laziness（智能体懒惰）**：复杂多部分任务中，智能体在只完成部分工作后宣称完成，例如安全 review 只处理了部分条目。
- **Self-preferential bias（自我偏好偏差）**：智能体在验证或按 rubric 评判时更偏向相信自己的结论。
- **Goal drift（目标漂移）**：长任务中原始目标保真度逐步下降，尤其在 compaction 后，边缘要求或 “不要做 X” 这类负约束会丢失。
- 来源把 dynamic workflow 的价值解释为：用各自拥有独立上下文窗口和聚焦目标的子智能体来对抗这些失败。

## 与已有 harness 机制的关系

- [[wiki/concepts/Self-verification|Self-verification]] 处理“写完就停”的问题，但对 self-preferential bias 仍不充分。
- [[wiki/concepts/External Evaluator Agent|External Evaluator Agent]] 通过独立判断者降低自评偏差。
- [[wiki/concepts/Goal Completion Contract|Goal Completion Contract]] 和 [[wiki/concepts/Evidence-Based Completion|Evidence-Based Completion]] 把完成判定绑定到可见证据，降低 agentic laziness。
- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]] 与 [[wiki/concepts/File-backed State|File-backed State]] 把关键约束外化，降低 compaction 造成的 goal drift。
- [[wiki/concepts/Dynamic Workflows|Dynamic Workflows]] 用多上下文、多角色和显式停止条件把这些机制按任务组合起来。

## 开放问题

- 如何用 trace 或日志自动检测 agentic laziness，而不是只靠人类事后发现？
- 对抗验证 agent 是否也会产生自己的 self-preferential bias？
- Goal drift 的最低成本防线是更强 completion contract、progress file，还是独立 verifier？
