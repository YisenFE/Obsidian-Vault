---
type: claim-set
status: draft
created: 2026-05-29
updated: 2026-05-29
aliases:
  - Deep agents harness engineering evidence and caveats
sources:
  - "[[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering]]"
tags:
  - llm-wiki/claim
  - langchain
  - harness-engineering
  - terminal-bench
---
# Deep Agents harness engineering 证据与注意事项

## 范围

本页追踪 [[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering|Improving Deep Agents with harness engineering]] 的关键论断，尤其是固定模型下的 harness 改动带来的 benchmark 增益、trace-driven iteration、自验证 middleware、上下文注入和推理预算分配。

## 来源支持的论断

| 论断 | 来源证据 | 状态 |
|---|---|---|
| 只改 harness 也能提升 Deep Agents 在 Terminal Bench 2.0 上的表现。 | 来源称固定 GPT-5.2-Codex，把分数从 52.8 提升到 66.5。 | 来源支持；未独立复现 |
| Trace analysis 可以指导 harness 改进。 | Trace Analyzer Skill 会抓取 LangSmith traces、并行派发错误分析 agent、综合发现并提出 harness 修改建议。 | 来源支持的流程 |
| Self-verification 需要显式强制进入循环。 | 常见失败是代码 review 后不测试就结束；`PreCompletionChecklistMiddleware` 会拦截退出并提醒验证。 | 来源支持 |
| 环境上下文注入可以降低错误面。 | `LocalContextMiddleware` 在任务开始前映射 cwd、父/子目录并发现本地工具。 | 来源支持的机制 |
| 循环检测能帮助从重复失败编辑中恢复。 | `LoopDetectionMiddleware` 统计每个文件的编辑次数，超过阈值后注入重新思考提示。 | 来源支持的启发式机制 |
| 推理强度不是越高越好。 | xhigh-only 因超时只得 53.9；high 得 63.6；xhigh-high-xhigh baseline 帮助达到 66.5。 | 来源支持，但依赖 benchmark |

## 注意事项 / 局限

- 数字来自 LangChain 自述，本 wiki 未复现 Terminal Bench run。
- Terminal Bench 有严格 timeout，因此部分经验与环境绑定。
- Trace-driven 改进可能过拟合 benchmark 任务；来源也明确提醒了这一点。
- Middleware 护栏针对的是当前模型短板，随着模型能力提升可能失效或变成冗余。
- Claude Opus 4.6 对比不是受控实验，因为 LangChain 没有对 Claude 运行同等 improvement loop。

## 后续待验证问题

| 问题 | 为什么重要 | 状态 |
|---|---|---|
| 13.7 分提升中，prompt、middleware、reasoning schedule 各贡献多少？ | 这决定哪些组件真正 load-bearing。 | 待验证 |
| Trace analyzer skill 是否提升真实仓库工作，而不只是 Terminal Bench？ | benchmark 迁移性不确定。 | 待验证 |
| Trace-driven 改动能否用 held-out task 检测过拟合？ | 这是可靠 harness 优化的关键。 | 待验证 |

## 相关页面

- [[wiki/concepts/Trace-driven Harness Iteration|Trace-driven Harness Iteration]]
- [[wiki/concepts/Build-Verify Loop|Build-Verify Loop]]
- [[wiki/concepts/Reasoning Budgeting|Reasoning Budgeting]]
- [[wiki/entities/products/Deep Agents|Deep Agents]]
- [[wiki/entities/products/Terminal Bench|Terminal Bench]]
