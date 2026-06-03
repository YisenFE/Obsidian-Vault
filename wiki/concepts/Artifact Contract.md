---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
  - "[[wiki/sources/2026-06-01 Using Goals in Codex]]"
tags:
  - llm-wiki/concept
  - verification
  - harness-engineering
---
# Artifact Contract

## 定义

产物契约（Artifact Contract）是 harness 对一次 agent run 应产出什么、如何记录证据、何时允许完成的约束。它可以表现为文件、测试结果、QA log、progress update、feature pass/fail 状态、benchmark answer 或其他可检查工件。

## 为什么重要

Agent 容易把“过程看起来合理”误判为“任务已经完成”。Artifact contract 把完成条件绑定到可审计工件，使 self-verification、session handoff 和 evaluator review 有共同依据。

## 来源支持的要点

- NLAH 论文把 artifact contracts 列为 IHR 解释执行的核心输出之一。
- RQ2 中 NLAH 在 Live-SWE 的 Artifact Contract 指标达到 1.000，在 MHTBA 上达到 0.955，说明 IHR 能把自然语言 contract 物化成可观察工件。
- Anthropic 的 feature list as test contract 是 artifact contract 的一个具体形式：agent 只能更新 `passes`，不能弱化测试描述。
- Anthropic planner/generator/evaluator harness 中的 sprint contract、evaluator feedback files 和 QA logs 也承担类似完成契约。

- Codex Goals 来源把 Goal 写法扩展成更一般的 completion contract：目标、验证面、约束、边界、迭代策略和阻塞停止条件。
- 与 NLAH artifact contract 类似，Goal 要求完成时能指向具体证据；预算到达或 blocker 出现时不能伪装成完成。

## 相关概念

- [[wiki/concepts/Feature List as Test Contract|Feature List as Test Contract]]
- [[wiki/concepts/Sprint Contract|Sprint Contract]]
- [[wiki/concepts/Self-verification|Self-verification]]
- [[wiki/concepts/Natural-Language Agent Harnesses|Natural-Language Agent Harnesses]]

- [[wiki/concepts/Goal Completion Contract|Goal Completion Contract]]
- [[wiki/concepts/Codex Goals|Codex Goals]]

## 开放问题

- Artifact contract 应该是自然语言描述、结构化 JSON/YAML，还是由测试/CI 自动生成？
- 如何防止 agent 修改契约本身来制造“完成”？
- 多 agent 阶段之间应共享同一 artifact contract，还是每个阶段有局部 contract？
