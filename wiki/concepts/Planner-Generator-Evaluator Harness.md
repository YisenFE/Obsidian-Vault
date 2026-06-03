---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
tags:
  - llm-wiki/concept
  - multi-agent
  - harness-engineering
---
# Planner-Generator-Evaluator Harness

## 定义

规划-生成-评估工作支架（Planner-Generator-Evaluator Harness）是一种多智能体 harness：planner 将短 prompt 扩展为高层产品规格，generator 根据规格构建应用，evaluator 以外部 QA/reviewer 身份检查结果并给出可执行反馈。

## 为什么重要

长时程应用开发同时有三个难点：短 prompt 容易 under-scope，单一 generator 容易失去连贯性或遗漏细节，自评又容易过度乐观。Planner / generator / evaluator 分工把“定目标、做实现、判质量”分开，使每个 agent 的 prompt 和工具更容易针对性调优。

## 来源支持的要点

- Anthropic 的 planner 接收 1–4 句 prompt，扩展为完整产品 spec，并被要求关注产品上下文和高层技术设计，而不是过早指定细粒度实现。
- Generator 在第一版 harness 中按 sprint 逐块实现 React/Vite/FastAPI/SQLite 或 PostgreSQL 应用，并在交给 QA 前做自评。
- Evaluator 使用 [[wiki/entities/products/Playwright MCP|Playwright MCP]] 像用户一样操作运行中的应用，同时检查 UI、API endpoint 和数据库状态。
- 第一版使用 sprint contract；后续在 [[wiki/entities/products/Claude Opus 4.6|Claude Opus 4.6]] 上移除 sprint construct，但保留 planner 和 evaluator。
- 作者把 generator/evaluator 分离类比为 GAN 式结构：生产者与判断者分开，使生成器可以基于外部反馈迭代。

## 相关概念

- [[wiki/concepts/External Evaluator Agent|External Evaluator Agent]]
- [[wiki/concepts/Sprint Contract|Sprint Contract]]
- [[wiki/concepts/Load-bearing Harness Components|Load-bearing Harness Components]]
- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/themes/长时程智能体工作流|Long-running agent workflows]]

## 开放问题

- Planner 应该多具体？过细会把错误传递给下游，过粗又可能无法形成可测边界。
- Evaluator 应该每 sprint 检查、每轮检查，还是只在最终阶段检查？
- 多智能体通信用文件是否足够，还是需要更结构化的消息/状态协议？
