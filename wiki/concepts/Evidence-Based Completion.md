---
type: concept
status: draft
created: 2026-06-01
updated: 2026-06-01
aliases:
  - Evidence-backed completion
  - Evidence decides completion
sources:
  - "[[wiki/sources/2026-06-01 Using Goals in Codex]]"
  - "[[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering]]"
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
tags:
  - llm-wiki/concept
  - verification
  - completion
  - evidence
---
# Evidence-Based Completion

## 定义

Evidence-Based Completion（证据驱动完成）是指 agent 不能因为“看起来完成”或“模型相信完成”而停止，必须用测试、benchmark、日志、文件 diff、artifact、报告或研究证据对照目标后，才能声明完成。

## 为什么重要

Agent 最常见失败之一是早停：代码已改就说完成，研究产物看起来合理就说复现成功，benchmark 改善但没达阈值也停止。证据驱动完成把“完成”从模型自信改成可审计判断。

## 来源支持的要点

- Codex Goals 来源说 completion must be evidence-based；目标要对照 files、tests、logs、benchmark output、generated artifacts 或 research evidence。
- Budget reached 不是完成；应报告 progress 和 blockers。
- LangChain Deep Agents 来源中，PreCompletionChecklistMiddleware 强制 agent 在完成前做 verification pass。
- NLAH 的 artifact contract 和 evidence-backed answering 也把完成绑定到可审计证据。

## 相关概念

- [[wiki/concepts/Self-verification|Self-verification]]
- [[wiki/concepts/Artifact Contract|Artifact Contract]]
- [[wiki/concepts/Goal Completion Contract|Goal Completion Contract]]
- [[wiki/concepts/Build-Verify Loop|Build-Verify Loop]]

## 开放问题

- 什么证据足以支持“完成”，什么只能支持“部分完成”？
- Evidence ledger 是否应成为所有长任务的标准产物？
- 当验证面本身 flaky 或不可运行时，Goal 应如何降级？
