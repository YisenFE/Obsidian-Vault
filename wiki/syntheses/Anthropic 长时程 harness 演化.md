---
type: synthesis
status: draft
created: 2026-05-29
updated: 2026-05-29
aliases:
  - Anthropic long-running harness evolution
sources:
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
tags:
  - llm-wiki/synthesis
  - anthropic
  - long-running-agents
  - harness-engineering
---
# Anthropic 长时程 harness 演化

## 综合结论

Anthropic 的两篇长时程智能体来源展示了一条演化线：先解决跨会话连续性（session continuity），再解决多智能体质量控制。早期 harness 用 initializer agent、coding agent、feature list、`claude-progress.txt`、git history 和 `init.sh` 处理“新上下文没有记忆”的问题；核心目标是可靠交接：每轮先理解当前状态，验证基础应用仍可运行，再实现一个增量，并留下干净状态。

后续 harness 继承了“分解工作、传递结构化工件”的直觉，但瓶颈变了：复杂应用和主观设计任务中，问题不只是交接，还包括范围界定不足、自我评价偏差和浅层 QA。对应方案是 planner/generator/evaluator 分离、sprint contract、校准后的设计标准，以及基于 Playwright 的外部评审。

## 变化点

| 维度 | 早期长时程 harness | 后续应用开发 harness |
|---|---|---|
| 主要失败模式 | 跨会话遗忘、一次性做太多、过早宣布完成 | 范围界定不足、context anxiety、自评偏乐观、QA 太浅 |
| 智能体角色 | Initializer + coding agent | Planner + generator + evaluator |
| 核心工件 | Feature list、progress file、git history、`init.sh` | 产品规格、sprint contract、evaluator 反馈文件、QA 日志 |
| 验证方式 | 标记 feature 通过前做浏览器自动化验证 | Evaluator 用 Playwright、评分标准和契约检查做外部评估 |
| 上下文策略 | 对有 context anxiety 的模型，用 context reset + handoff | 模型能力允许时，连续会话 + 自动 compaction 即可 |
| 设计原则 | 让每轮会话可恢复、可验证、可合并 | 分离规格、生成和判断；随着模型能力提升而简化 |

## 综合启发

长时程 harness 不是固定 recipe。它通常从外化记忆和任务状态开始，只在当前模型确实失败的地方增加专门角色。模型能力提升后，部分脚手架会变成开销；但可靠基线向外扩展后，团队也能尝试更复杂、更长期的 harness。

## 开放问题

- 跨会话 handoff 工件和 evaluator 反馈能否统一为一种持久项目记忆格式？
- harness 应该如何动态选择 solo、planner+generator、完整 planner+generator+evaluator 三种模式？
- 什么 benchmark 能区分 harness 本身的价值和“只是花了更多 token/时间”的效果？
