---
type: source-summary
status: ingested
created: 2026-05-29
updated: 2026-05-29
source: "[[raw/2026-05-28 Improving Deep Agents with harness engineering]]"
external_url: https://www.langchain.com/blog/improving-deep-agents-with-harness-engineering
author: "[[wiki/entities/people/Vivek Trivedy|Vivek Trivedy]]"
published: 2026-02-18
image_assets:
  - "[[raw/assets/2026-05-28-langchain-terminal-bench-score.png]]"
  - "[[raw/assets/2026-05-28-langchain-baseline-score.png]]"
  - "[[raw/assets/2026-05-28-langchain-trace-analyzer-skill.png]]"
  - "[[raw/assets/2026-05-28-langchain-self-verification-loop.png]]"
  - "[[raw/assets/2026-05-28-langchain-reasoning-sandwich.png]]"
tags:
  - llm-wiki/source
  - langchain
  - harness-engineering
  - deep-agents
  - terminal-bench
---
# Improving Deep Agents with harness engineering

## 一句话结论

LangChain 把 harness engineering 做成可迭代实验流程：固定模型 [[wiki/entities/products/GPT-5.2-Codex|GPT-5.2-Codex]]，只调整 system prompt、tools 和 middleware，通过 [[wiki/entities/products/LangSmith|LangSmith]] traces 分析失败模式，在 [[wiki/entities/products/Terminal Bench|Terminal Bench 2.0]] 上把 [[wiki/entities/products/Deep Agents|deepagents-cli]] 从 52.8% 提升到 66.5%。

## 来源元数据

- 原始资料： [[raw/2026-05-28 Improving Deep Agents with harness engineering]]
- 外部链接： [LangChain — Improving Deep Agents with harness engineering](https://www.langchain.com/blog/improving-deep-agents-with-harness-engineering)
- 作者： [[wiki/entities/people/Vivek Trivedy|Vivek Trivedy]]
- 发表时间： 2026-02-18
- 本地图片资产（ingest 时已读取）：
  - Terminal Bench 排行榜： ![[raw/assets/2026-05-28-langchain-terminal-bench-score.png]]
  - Baseline / improvement 表： ![[raw/assets/2026-05-28-langchain-baseline-score.png]]
  - Trace analyzer skill 图： ![[raw/assets/2026-05-28-langchain-trace-analyzer-skill.png]]
  - Self-verification loop 图： ![[raw/assets/2026-05-28-langchain-self-verification-loop.png]]
  - Reasoning sandwich 图： ![[raw/assets/2026-05-28-langchain-reasoning-sandwich.png]]

## 关键要点

1. 文章把 harness engineering 定义为围绕模型构建系统，优化 task performance、token efficiency、latency 等目标；可调 knob 包括 system prompt、tool choice、execution flow、hooks/middleware、skills、sub-agent delegation、memory systems。
2. LangChain 为了压缩优化空间，重点调整三类 knob：System Prompt、Tools、[[wiki/concepts/Middleware Hooks|Middleware]]；模型固定为 [[wiki/entities/products/GPT-5.2-Codex|GPT-5.2-Codex]]。
3. 实验环境是 [[wiki/entities/products/Terminal Bench|Terminal Bench 2.0]]：89 个跨机器学习、debugging、生物等领域的 agentic coding 任务；[[wiki/entities/products/Harbor|Harbor]] 负责编排 run、启动 [[wiki/entities/products/Daytona|Daytona]] sandbox、交互 agent loop、运行验证和打分。
4. 所有 agent action 存入 [[wiki/entities/products/LangSmith|LangSmith]]，并带有 latency、token count、cost 等指标；traces 是分析黑盒模型失败模式的主要可观测性来源。
5. [[wiki/concepts/Trace-driven Harness Iteration|Trace-driven Harness Iteration]] 的流程是：抓取 LangSmith experiment traces，并行派发 error analysis agents，主 agent 综合发现和建议，再由人类或 agent 做 targeted harness changes。
6. 最常见失败模式是 agent 写出方案、重读自己代码、觉得没问题就停止；LangChain 通过 system prompt 和 `PreCompletionChecklistMiddleware` 强制 agent 进入 [[wiki/concepts/Build-Verify Loop|Build-Verify Loop]]。
7. Build-verify prompt 包含 Planning & Discovery、Build、Verify、Fix 四步，强调测试 happy path 和 edge cases，并且验证要对照任务 spec，而不是只对照 agent 自己写的代码。
8. [[wiki/concepts/Local Context Injection|Local Context Injection]] 通过 `LocalContextMiddleware` 在 agent 启动时映射 cwd、父/子目录，查找 Python 等可用工具，降低环境探索错误面。
9. Prompt 还会教 agent 写可测试代码：遵守 task spec 中的文件路径、面向程序化评分、重视 edge cases，避免只检查 happy path。
10. Time budget warnings 帮 agent 在 Terminal Bench 严格 timeout 中及时从构建转向验证；这是一种环境约束注入。
11. `LoopDetectionMiddleware` 通过 tool-call hooks 跟踪每个文件的编辑次数，在同一文件编辑超过 N 次后提醒 agent 重新考虑方案，以打断 “doom loops”。
12. [[wiki/concepts/Reasoning Budgeting|Reasoning Budgeting]] 是另一类 harness knob：LangChain 使用 xhigh-high-xhigh “reasoning sandwich”，在计划和最终验证阶段投入更多推理，在中间构建阶段节约时间/成本。
13. 文章报告的分数：baseline 52.8%；加入 custom prompt & middleware 后 63.6%；再加入 reasoning sandwich 后 66.5%，Terminal Bench 2.0 排名约 Top 5。只用 xhigh reasoning 反而因超时只得 53.9%，high 得 63.6%。
14. LangChain 强调 harness 要针对模型调优：Claude Opus 4.6 在早期 harness 上测试为 59.6%，但作者认为未对 Claude 做同等 improvement loop，因此不能简单归因于模型能力差异。
15. 开放方向包括 multi-model harness、memory primitives for continual learning、跨模型测量 harness changes，以及用 RLMs 更高效地挖掘 traces。

## 需要更新的概念

- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Trace-driven Harness Iteration|Trace-driven Harness Iteration]]
- [[wiki/concepts/Build-Verify Loop|Build-Verify Loop]]
- [[wiki/concepts/Middleware Hooks|Middleware Hooks]]
- [[wiki/concepts/Local Context Injection|Local Context Injection]]
- [[wiki/concepts/Reasoning Budgeting|Reasoning Budgeting]]
- [[wiki/concepts/Feedback Sensors|Feedback Sensors]]
- [[wiki/concepts/Self-verification|Self-verification]]
- [[wiki/concepts/Load-bearing Harness Components|Load-bearing Harness Components]]

## 需要更新的实体

- 人物： [[wiki/entities/people/Vivek Trivedy|Vivek Trivedy]]
- 组织： [[wiki/entities/organizations/LangChain|LangChain]], [[wiki/entities/organizations/OpenAI|OpenAI]], [[wiki/entities/organizations/Anthropic|Anthropic]]
- 产品/工具： [[wiki/entities/products/Deep Agents|Deep Agents]], [[wiki/entities/products/LangSmith|LangSmith]], [[wiki/entities/products/Terminal Bench|Terminal Bench]], [[wiki/entities/products/Harbor|Harbor]], [[wiki/entities/products/Daytona|Daytona]], [[wiki/entities/products/GPT-5.2-Codex|GPT-5.2-Codex]], [[wiki/entities/products/Claude Opus 4.6|Claude Opus 4.6]]

## 论断 / 证据

| 论断 | 证据 | 置信度 |
|---|---|---:|
| 只改 harness 也能显著提升 benchmark 表现。 | 来源称固定 GPT-5.2-Codex，把 Terminal Bench 2.0 分数从 52.8 提升到 66.5。 | 中高：来源支持，未复现 |
| Trace analysis 是 harness 迭代有效的外循环反馈信号。 | LangChain 把每个 action 存入 LangSmith，并构建 trace analyzer skill 聚合错误模式、建议 harness 改动。 | 高：来源支持的流程 |
| Self-verification 需要主动 prompt 与 hook。 | 最常见失败是代码 review 后不测试就停止；`PreCompletionChecklistMiddleware` 拦截退出并提醒验证。 | 高 |
| Context injection 可以降低环境探索错误。 | `LocalContextMiddleware` 在 agent 开始前映射目录并发现工具。 | 高：来源支持的机制 |
| Reasoning budget 应被分配，而不是全程拉满。 | xhigh-only 因 timeout 得 53.9；high 得 63.6；最终策略使用 xhigh-high-xhigh 达到 66.5。 | 中高：依赖 benchmark |
| Harness 应针对模型调优。 | Claude Opus 4.6 在早期 harness 上得 59.6，但作者提醒并未对 Claude 跑同等 improvement loop。 | 高：警示原则 |

## 冲突 / 注意事项

- Benchmark 数字来自 LangChain 自述，本次 ingest 未复现 Terminal Bench run。
- 改进循环有过拟合 benchmark task 的风险；来源明确说 task-specific overfit 会损害泛化。
- Terminal Bench 有严格 timeout，因此 time-budget 与 reasoning-budget 经验不一定能原样迁移到没有硬时间限制的真实 coding。
- loop detection 等 middleware guardrails 针对今天的模型短板，模型提升后可能变得不必要。
- 来源使用其语境中的未来/当前模型名；本 wiki 将其作为来源支持的实体处理，不把它们当作独立验证过的产品事实。

## 后续问题

- LangChain 的提升中，prompt changes、middleware、reasoning schedule 分别贡献多少？
- Trace analyzer skill 能否泛化到非 benchmark 的团队仓库，并避免过拟合？
- Trace-driven harness iteration 应如何与 Böckeler 的 feedforward/feedback user-harness 模型结合？
