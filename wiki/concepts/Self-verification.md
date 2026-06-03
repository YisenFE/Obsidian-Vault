---
type: concept
status: draft
created: 2026-05-29
updated: 2026-06-03
sources:
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
  - "[[wiki/sources/2026-05-28 工程技术：在智能体优先的世界中利用 Codex]]"
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
  - "[[wiki/sources/2026-05-28 Harness engineering for coding agent users]]"
  - "[[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering]]"
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
  - "[[wiki/sources/2026-06-01 Using Goals in Codex]]"
  - "[[wiki/sources/2026-06-03 A harness for every task dynamic workflows in Claude Code]]"
tags:
  - llm-wiki/concept
  - verification
  - testing
  - agent-feedback
---
# Self-verification

## 定义

自验证（Self-verification）是让 agent 在声明完成前主动运行可观察、可复现的检查，并基于检查结果修复自身输出。它强调“从 spec/用户视角验证行为”，并把快速反馈尽量放进 agent 自修正循环，而不是只依赖最终人类 review。

## 为什么重要

Agent 容易把“代码已改”误认为“功能已完成”。在长时程任务中，错误状态还会被下一轮继承并放大。自验证把完成判定绑定到可执行证据，降低半成品、假阳性和跨 session 漂移。

## 来源支持的要点

- Anthropic 早期文章观察到 Claude 会在缺少明确提示时过早标记 feature 完成，即便没有端到端验证。
- OpenAI 的 Codex-first 来源强调把 DOM、截图、导航、日志、指标和 trace 暴露给 agent，让 Codex 能复现、修复并重新验证。
- Anthropic harness design 文章给出重要修正：self-verification 不等于可靠 evaluation。Agent 自评容易过度乐观，因此复杂/主观任务可能需要 [[wiki/concepts/External Evaluator Agent|External Evaluator Agent]]。
- Böckeler 来源把 self-correction loop 放在 change lifecycle 中：`/code-review`、eslint、semgrep、coverage、dep-cruiser 等 sensors 可在 integration 前反馈给 coding agent。
- LangChain 来源把 self-verification 具体化为 [[wiki/concepts/Build-Verify Loop|Build-Verify Loop]]：Planning & Discovery、Build、Verify、Fix。
- LangChain 使用 `PreCompletionChecklistMiddleware` 在 agent 退出前强制提醒它对 task spec 做 verification pass，避免写完代码后只读代码就停。
- LangChain 强调 Verify 要运行测试、读完整输出，并对照任务 spec 而不是对照 agent 自己写的代码。

- NLAH 论文把 [[wiki/concepts/Artifact Contract|Artifact Contract]] 作为 IHR 执行的核心机制之一，并在 RQ2 中用 contract compliance、tool-call success 和 failed-tool continuation 指标证明 policy 被物化。
- RQ3 中 evidence-backed answering 与 verifier 模块说明：验证只有贴近 benchmark gate 或任务验收标准时才有效；脱离验收语境的验证可能只增加过程成本。
- LangChain Anatomy 来源强调，browser、logs、screenshots 和 test runners 给 agent 观察/分析自身工作的能力，是 self-verification loop 的环境基础。
- 文章把 planning 与 self-verification 放在 long-horizon execution 中：agent 完成每一步后应对照正确性检查，失败则修复。
- Harness 可以用 hook 运行预定义测试并把错误回传给模型，也可以 prompt 模型独立评估自己的代码。

- Claude Code shorthand 来源中的 `/tdd`、`/e2e`、`/test-coverage`、PostToolUse `tsc --noEmit` 和 GitHub Actions PR review 都是把验证放进 Claude Code 工作流的例子。
- Stop hook 审计修改文件可以作为“声明完成前”的最后检查。

- Codex Goals 来源进一步强调，completion 必须 evidence-based：文件、测试、日志、benchmark、生成 artifact 或研究证据决定是否完成。
- Goal 把 self-verification 从“本轮结束前检查”提升为跨 turn 的完成条件；如果 p95 仍未达标或 correctness suite 失败，Goal 不应完成。

- Claude Code dynamic workflows 来源把 self-verification 的不足显式化：单 agent 验证自己容易出现 self-preferential bias，因此复杂任务可让 workflow 为每个结果派独立 adversarial verifier。
- Deep verification 用例建议先由 agent 找出报告中的事实性 claims，再逐项派子智能体查证，并可再用 verification agent 检查来源质量。

## 相关概念

- [[wiki/concepts/Artifact Contract|Artifact Contract]]
- [[wiki/concepts/Natural-Language Agent Harnesses|Natural-Language Agent Harnesses]]
- [[wiki/concepts/Build-Verify Loop|Build-Verify Loop]]
- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Feedback Sensors|Feedback Sensors]]
- [[wiki/concepts/Behaviour Harness|Behaviour Harness]]
- [[wiki/concepts/External Evaluator Agent|External Evaluator Agent]]
- [[wiki/concepts/Middleware Hooks|Middleware Hooks]]

- [[wiki/concepts/Evidence-Based Completion|Evidence-Based Completion]]
- [[wiki/concepts/Dynamic Workflows|Dynamic Workflows]]
- [[wiki/concepts/Long-running Agent Failure Modes|Long-running Agent Failure Modes]]

## 开放问题

- 哪些检查必须由 generator 自己运行，哪些应交给独立 evaluator/QA agent？
- 自验证证据应如何记录，才能被下一轮 session 复用？
- 如何避免 agent 写低质量测试来满足自己的自验证循环？
- 对抗式 verifier 的 false positive 和 token 成本应如何纳入 completion contract？
