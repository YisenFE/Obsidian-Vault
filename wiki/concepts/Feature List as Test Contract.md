---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
tags:
  - llm-wiki/concept
  - testing
  - requirements
  - harness-engineering
---
# Feature List as Test Contract

## 定义

作为测试契约的功能清单（Feature List as Test Contract）是把用户目标扩展成结构化、可逐项验收的功能清单，并把它当作 agent 不可随意改写的测试契约。Agent 可以实现功能并更新通过状态，但不能通过删除、弱化或重写验收条件来制造“完成”。

## 为什么重要

长时程 agent 容易 one-shot 复杂任务，也容易在已有局部进展后过早宣布完成。完整 feature list 把“最终完成长什么样”外化成可追踪契约，迫使每轮 agent 只选择一个未完成功能并在验证后更新状态。

## 来源支持的要点

- Anthropic 的 initializer agent 会根据高层 prompt 写出覆盖完整应用目标的 feature requirements。
- 在 claude.ai clone 示例中，feature list 超过 200 项，并全部初始标记为 failing。
- Coding agents 被要求只修改 `passes` 字段，不得删除或编辑测试描述。
- Anthropic 选择 JSON 而不是 Markdown，因为他们观察到模型更不容易不当改写或覆盖 JSON 文件。
- Feature list 同时解决两个失败模式：agent 试图一次性做完，以及 agent 过早认为项目完成。
- 后续 planner/generator/evaluator harness 把这一思想细化为 [[wiki/concepts/Sprint Contract|Sprint Contract]]：每个 chunk 在实现前先协商 “done” 和验收 criteria。

## 相关概念

- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Mechanized Invariants|Mechanized Invariants]]
- [[wiki/concepts/Self-verification|Self-verification]]
- [[wiki/concepts/Sprint Contract|Sprint Contract]]
- [[wiki/themes/长时程智能体工作流|Long-running agent workflows]]

## 开放问题

- Feature list 应该由 initializer 一次性生成，还是由 planner/evaluator 多轮修订？
- JSON 契约是否适合非软件项目，例如研究计划或财务模型？
- 如何防止 agent 只做“让测试变绿”的表面实现？
