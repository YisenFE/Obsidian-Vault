---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
tags:
  - llm-wiki/concept
  - testing
  - requirements
  - multi-agent
---
# Sprint Contract

## 定义

Sprint 契约（Sprint Contract）是 generator 与 evaluator 在实现某个工作 chunk 前共同确认的“完成定义”：包含本轮要构建什么、如何验证、哪些行为必须通过，以及哪些实现细节暂不提前规定。

## 为什么重要

高层 product spec 可以保持灵活，但直接让 generator 开工会留下过大的解释空间。Sprint contract 在 user story 与可测试实现之间加一层协议，让 evaluator 在编码前先确认方向，编码后再按同一契约验收。

## 来源支持的要点

- Anthropic 第一版 full-stack harness 在每个 sprint 前让 generator 提议构建内容和成功验证方式。
- Evaluator 审查该提议，确保 generator 正在构建正确内容；双方通过文件迭代直到达成一致。
- 这种契约避免 planner 过早规定细节，又避免 generator 按自己的理解偏离产品目标。
- Retro game maker 示例中，Sprint 3 有 27 条覆盖 level editor 的验收 criteria，evaluator 能逐条发现具体 bug。
- 后续 Opus 4.6 简化版移除了 sprint construct，说明 sprint contract 是模型/任务相关的承重组件，而非永久必需。

## 相关概念

- [[wiki/concepts/Feature List as Test Contract|Feature List as Test Contract]]
- [[wiki/concepts/Planner-Generator-Evaluator Harness|Planner-Generator-Evaluator Harness]]
- [[wiki/concepts/External Evaluator Agent|External Evaluator Agent]]
- [[wiki/concepts/Load-bearing Harness Components|Load-bearing Harness Components]]

## 开放问题

- Sprint contract 应该是自然语言、JSON，还是测试代码/BDD spec？
- 谁有权修改 contract：planner、generator、evaluator，还是人类？
- 当模型能力提升后，移除 sprint contract 的判断标准是什么？
