---
type: concept
status: draft
created: 2026-06-03
updated: 2026-06-03
aliases:
  - Claude Code dynamic workflows
  - Task-specific dynamic harnesses
  - Dynamic agent workflows
sources:
  - "[[wiki/sources/2026-06-03 A harness for every task dynamic workflows in Claude Code]]"
tags:
  - llm-wiki/concept
  - claude-code
  - dynamic-workflows
  - multi-agent
  - harness-engineering
---
# Dynamic Workflows

## 定义

Dynamic Workflows（动态工作流）是 Claude Code 中由 Claude 为当前任务现场生成和执行的多智能体 workflow。它通常体现为一段 JavaScript orchestration：用特殊函数 spawn / coordinate subagents，用标准 JavaScript 处理数据，并按任务决定模型、worktree 隔离、验证步骤和停止条件。

## 为什么重要

传统静态 workflow 要提前写好并覆盖很多边界情况，因此容易变得通用、笨重或不贴合当前任务。Dynamic workflow 的价值在于把 harness 变成 task-specific custom harness（面向任务的定制工作支架）：复杂任务需要分发、对抗验证、排序、循环或模型路由时，Claude 可以即时搭一个结构，而不是把计划和执行都塞进同一个上下文窗口。

## 来源支持的要点

- Claude Code 默认 harness 适合很多 coding task，但长时程、大规模并行、高结构化或对抗性任务会暴露单上下文限制。
- Dynamic workflow 可决定每个子智能体使用的模型，以及是否在自己的 worktree 中运行。
- workflow 被中断后，恢复 session 时可继续执行，适合长任务和可恢复执行。
- 文章强调 dynamic workflows 往往更耗 token，最适合复杂、高价值任务；常规 coding task 不一定需要多评审或额外 compute。
- workflow 可以保存到 `~/.claude/workflows`，也可以通过 skill 分发，但 skill 中的 workflow 更适合作为模板而非必须逐字执行的脚本。

## 常见模式

| 模式 | 中文解释 | 适用场景 |
|---|---|---|
| Classify-and-act | 先分类再行动 | 任务类型不同、需要路由到不同 agent 或流程。 |
| Fan-out-and-synthesize | 分发并综合 | 大量小任务、各子任务需要干净上下文，最后合并结构化输出。 |
| Adversarial verification | 对抗式验证 | 需要独立 agent 按 rubric 检查每个结果，降低自评偏差。 |
| Generate-and-filter | 生成并筛选 | 命名、设计、方案探索、候选项去重与筛选。 |
| Tournament | 锦标赛式比较 | 多方案竞争、pairwise judgment 比绝对评分更可靠的排序任务。 |
| Loop until done | 循环直到完成 | 工作量未知，停止条件是没有新发现、日志无错误或验收标准通过。 |

## 典型用例

- 迁移和重构：按 callsite、失败测试、模块拆分，让子智能体在 worktree 中修复，再由另一个 agent review。
- Deep research：并行搜索/抓取来源，对声明做对抗验证，再综合带引用报告。
- Deep verification：先识别事实性 claims，再逐项派发子智能体查证，并可再用 verification agent 审查来源质量。
- 规则遵守和记忆挖掘：从最近 session 或 code review 反馈中聚类反复出现的纠正，再验证哪些规则能防止真实错误。
- 根因调查：让不同 agent 从日志、文件、数据等不同证据面提出假设，再互相反驳和验证。
- 大规模 triage：分类、去重、尝试修复或升级给人类；读取不可信内容的 agent 应与执行高权限动作的 agent 隔离。
- Evals 与模型路由：在 worktree 中并行评估任务输出，并用 classifier agent 决定 Sonnet / Opus 等模型选择。

## 相关概念

- [[wiki/concepts/Claude Code Operating Harness|Claude Code Operating Harness]]
- [[wiki/concepts/Subagent Scoping|Subagent Scoping]]
- [[wiki/concepts/Parallel Agent Workflows|Parallel Agent Workflows]]
- [[wiki/concepts/External Evaluator Agent|External Evaluator Agent]]
- [[wiki/concepts/Self-verification|Self-verification]]
- [[wiki/concepts/Agent Rules and Memory|Agent Rules and Memory]]
- [[wiki/concepts/Long-running Agent Failure Modes|Long-running Agent Failure Modes]]
- [[wiki/concepts/Context Reset vs Compaction|Context Reset vs Compaction]]

## 开放问题

- 何时把一次性 dynamic workflow 保存为长期 workflow 或 skill？
- workflow 的并行度、模型路由、worktree 使用和 token budget 应如何自动调参？
- 对抗式 verification 的成本与收益如何度量？
- workflow 读取 Slack、网页、issue 等不可信内容时，权限隔离应如何表达和执行？
