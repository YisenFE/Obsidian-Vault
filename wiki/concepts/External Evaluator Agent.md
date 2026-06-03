---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
  - "[[wiki/sources/2026-05-28 Harness engineering for coding agent users]]"
tags:
  - llm-wiki/concept
  - evaluation
  - qa
  - multi-agent
---
# External Evaluator Agent

## 定义

外部评估智能体（External Evaluator Agent）是与执行 agent 分离的判断者：它不负责主要实现，而是使用独立 prompt、标准和工具检查输出质量，给出具体失败点和下一轮修复反馈。按 Böckeler 的分类，它通常是一类 inferential feedback sensor。

## 为什么重要

Agent 自评通常过度乐观，容易把可运行或看起来不错误判为高质量完成。把评价者独立出来，可以更集中地调优怀疑精神、测试深度和评分标准，让 generator 面对外部反馈而不是自我背书。

## 来源支持的要点

- Anthropic harness design 文章指出，agent 评价自己的输出时常会自信地夸奖，即使人类观察者觉得质量普通。
- 对主观设计任务，作者把 design quality、originality、craft、functionality 写成可评分标准，并用 few-shot 示例校准 evaluator。
- 对 full-stack app，evaluator 通过 [[wiki/entities/products/Playwright MCP|Playwright MCP]] 操作页面，并检查 UI feature、API endpoint、数据库状态和代码质量。
- QA agent 初始并不可靠：它会发现真实问题后说服自己“问题不大”并通过；需要阅读 trace 并持续更新 QA prompt。
- Böckeler 来源把 review agents/LLM-as-judge 归为 inferential sensors：适合语义判断，但更慢、更贵、更非确定，需要按生命周期和风险放置。
- Evaluator 的价值依赖任务是否超出当前 generator model 的 solo 稳定能力边界；不是固定必需组件。

## 相关概念

- [[wiki/concepts/Self-verification|Self-verification]]
- [[wiki/concepts/Feedback Sensors|Feedback Sensors]]
- [[wiki/concepts/Computational and Inferential Controls|Computational and Inferential Controls]]
- [[wiki/concepts/Planner-Generator-Evaluator Harness|Planner-Generator-Evaluator Harness]]
- [[wiki/concepts/Load-bearing Harness Components|Load-bearing Harness Components]]

## 开放问题

- Evaluator 的评分标准如何避免把个人审美过拟合为通用质量？
- Evaluator 应该拥有比 generator 更多、更少，还是不同的工具权限？
- 哪些任务值得 external evaluation，哪些只需要 generator self-check？
