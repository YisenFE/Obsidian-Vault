---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
  - "[[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering]]"
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
tags:
  - llm-wiki/concept
  - harness-engineering
  - model-capability
---
# Load-bearing Harness Components

## 定义

承重型工作支架组件（Load-bearing Harness Components）是那些对当前模型、任务和质量目标确实贡献结果的 harness 组件。一个组件是否承重不是永久属性，而会随模型能力、任务难度、工具环境、评估目标和成本约束变化。

## 为什么重要

复杂 harness 往往昂贵、慢、难维护。每个组件都隐含一个假设：模型自己做不好某件事。随着模型提升，这些假设可能过期；反过来，更强模型也可能让新的复杂任务成为可能，从而需要新的承重组件。

## 来源支持的要点

- Anthropic 作者认为，维护 harness 时应逐个 stress test 组件，而不是默认保留所有脚手架。
- [[wiki/entities/products/Claude Opus 4.6|Claude Opus 4.6]] 的能力提升后，sprint construct 不再总是必要，但 planner/evaluator 在某些边界任务上仍然承重。
- LangChain 来源以 benchmark 实验更直接地检验组件：baseline 52.8，custom prompt & middleware 后 63.6，再加入 reasoning schedule 后 66.5。
- LangChain 的 `PreCompletionChecklistMiddleware`、`LocalContextMiddleware`、`LoopDetectionMiddleware` 和 time budget warnings 都是围绕当前模型/benchmark 失败模式的组件。
- LangChain 同时提醒这些 guardrails 是针对 today’s perceived model issues，随着模型改进可能不再需要。
- [[wiki/concepts/Reasoning Budgeting|Reasoning Budgeting]] 也是承重性问题：xhigh-only 因 timeout 反而差于 high，说明“更多推理”并非无条件承重。

- NLAH 论文提供了更直接的 module ablation 框架：在同一 IHR 下加入 file-backed state、evidence-backed answering、verifier、self-evolution、multi-candidate search、dynamic orchestration、context compression、markdown memory 等模块，观察 performance 与 agent calls 变化。
- 结果显示，能让 state、evidence 与 acceptance path 更清晰的模块更可能承重；只增加分支或局部流程层的模块可能增加成本却不提升结果。
- LangChain Anatomy 来源提供了“行为倒推组件”的承重判断框架：如果模型无法独立完成某种行为，就需要一个对应 harness feature；当模型能力吸收该行为，组件承重性可能下降。
- Model-harness co-evolution 也说明，组件承重性会随训练循环变化：primitive 被加入 harness 后可能进入模型后训练，后来模型更擅长该 primitive，但也更可能依赖具体工具协议。

## 相关概念

- [[wiki/concepts/Harness Module Ablation|Harness Module Ablation]]
- [[wiki/concepts/File-backed State|File-backed State]]
- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Trace-driven Harness Iteration|Trace-driven Harness Iteration]]
- [[wiki/concepts/Middleware Hooks|Middleware Hooks]]
- [[wiki/concepts/Reasoning Budgeting|Reasoning Budgeting]]

- [[wiki/concepts/Model-Harness Co-evolution|Model-Harness Co-evolution]]
- [[wiki/concepts/Agent Harness|Agent Harness]]

## 开放问题

- 如何低成本判断一个组件是否真的承重？
- Harness 组件评估应看最终质量、成本、延迟、可维护性，还是失败恢复能力？
- 当模型更新时，团队应多频繁重测旧 harness？
