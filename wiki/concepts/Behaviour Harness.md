---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Harness engineering for coding agent users]]"
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
  - "[[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering]]"
tags:
  - llm-wiki/concept
  - harness-engineering
  - behaviour
  - testing
---
# Behaviour Harness

## 定义

行为工作支架（Behaviour Harness）是用生成前引导（feedforward guides）和生成后反馈检测器（feedback sensors）调节应用功能行为是否符合需求的 harness：它试图回答“应用是否真的做了用户需要的事”。

## 为什么重要

可维护性和架构漂移有较多确定性工具可以检测，但功能行为往往依赖需求表达、测试质量、用户体验和人工判断。Coding agent 自己生成测试再让测试通过，并不能充分证明行为正确。

## 来源支持的要点

- Böckeler 将 behaviour harness 称为 “elephant in the room”。
- 常见做法是 feed-forward 一份功能规格，再让 AI 生成测试套件、跑 coverage/mutation testing，并结合人工测试。
- 文章认为这种做法过度信任 AI 生成测试，尚不足以显著减少监督。
- Anthropic 早期 long-running harness 用 feature list + browser automation 改善行为验证。
- Anthropic planner/generator/evaluator harness 用 sprint contract + Playwright evaluator 进一步把功能行为变成可验收 criteria，但仍承认 QA 覆盖有上限。
- LangChain 的 Terminal Bench 场景把行为正确性外化为 task spec、测试、程序化评分和 benchmark result；这让 build-verify loop 有清晰 hill-climb 信号。
- LangChain 也强调 agent 要对照原始 task spec 验证，而不是对照自己写的代码。

## 相关概念

- [[wiki/concepts/Harness Regulation Categories|Harness Regulation Categories]]
- [[wiki/concepts/Build-Verify Loop|Build-Verify Loop]]
- [[wiki/concepts/Feature List as Test Contract|Feature List as Test Contract]]
- [[wiki/concepts/Sprint Contract|Sprint Contract]]
- [[wiki/concepts/Self-verification|Self-verification]]

## 开放问题

- 如何验证 AI 生成测试本身的质量？
- Behaviour harness 的“覆盖率”应该如何定义？
- Benchmark-style scoring 能迁移到普通产品开发到什么程度？
