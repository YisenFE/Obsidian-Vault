---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Harness engineering for coding agent users]]"
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
  - "[[wiki/sources/2026-05-28 工程技术：在智能体优先的世界中利用 Codex]]"
  - "[[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering]]"
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
tags:
  - llm-wiki/concept
  - harness-engineering
  - feedback
  - verification
---
# Feedback Sensors

## 定义

生成后反馈检测器（Feedback Sensors）是在 agent 生成、修改或运行之后检测问题的机制，并把结果反馈给 agent、人类、pipeline 或 harness-improvement loop，以触发自修正、阻断、审查或后续改进。

## 为什么重要

Agent 生成的代码不能只靠最终人类 review 才发现问题。便宜快速的 sensors 可以进入 agent 自修正循环；昂贵广域的 sensors 可以放到 integration、pipeline、连续健康监控或 trace 分析外循环中。

## 来源支持的要点

- Böckeler 的例子包括 review agents、static analysis、logs、browser、eslint、semgrep、coverage、dep-cruiser、architecture-review、detailed-review、mutation testing。
- Feedback sensors 可以是 computational 的，也可以是 inferential 的；前者可靠快速，后者更适合语义判断但成本和不确定性更高。
- Anthropic planner/generator/evaluator harness 中的 evaluator 是一种 inferential feedback sensor，使用 Playwright 操作应用并提出 QA 反馈。
- OpenAI Codex-first 来源中的 DOM、截图、日志、指标和 trace 是 runtime feedback sensors，进入 reproduce-fix-verify 循环。
- LangChain 来源把 LangSmith traces 升级为 harness 外循环的 feedback sensor：不仅检查一次变更，还分析大量 run 的失败模式并指导下一轮 harness 修改。
- `PreCompletionChecklistMiddleware`、`LoopDetectionMiddleware` 和 time budget warnings 体现了 feedback sensor 与 middleware hook 的结合。

- Claude Code shorthand 来源中的 hooks 是用户侧 feedback sensors：PostToolUse 可运行 formatter/typecheck，Stop 可审计修改文件，GitHub Actions 可让 Claude 对 PR 自动 review。
- tmux + logs 则把长命令运行状态暴露给人类和 agent，增强长任务观察面。

## 相关概念

- [[wiki/concepts/Feedforward Guides|Feedforward Guides]]
- [[wiki/concepts/Computational and Inferential Controls|Computational and Inferential Controls]]
- [[wiki/concepts/Self-verification|Self-verification]]
- [[wiki/concepts/Trace-driven Harness Iteration|Trace-driven Harness Iteration]]
- [[wiki/concepts/Middleware Hooks|Middleware Hooks]]

- [[wiki/concepts/Claude Code Hooks|Claude Code Hooks]]

## 开放问题

- Sensors 从未触发时，是质量很高，还是探测能力不足？
- 如何评估 feedback sensor 覆盖率和质量？
- 哪些 sensors 应该由 agent 每次运行，哪些应该只在 CI、trace 分析或定期任务中运行？
