---
type: synthesis
status: draft
created: 2026-05-29
updated: 2026-06-05
aliases:
  - Anthropic long-running harness evolution
sources:
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
  - "[[wiki/sources/2026-06-03 A harness for every task dynamic workflows in Claude Code]]"
  - "[[wiki/sources/2026-06-06 Agents that remember]]"
tags:
  - llm-wiki/synthesis
  - anthropic
  - long-running-agents
  - harness-engineering
---
# Anthropic 长时程 harness 演化

## 综合结论

Anthropic 的长时程智能体来源展示了一条演化线：先解决跨会话连续性（session continuity），再解决多智能体质量控制，再把多智能体 harness 变成 Claude Code 内可按任务动态生成的 workflow，最后把跨 session memory 和 memory maintenance 产品化为 Claude Managed Agents 的 memory stores 与 dreaming。早期 harness 用 initializer agent、coding agent、feature list、`claude-progress.txt`、git history 和 `init.sh` 处理“新上下文没有记忆”的问题；核心目标是可靠交接：每轮先理解当前状态，验证基础应用仍可运行，再实现一个增量，并留下干净状态。

后续 harness 继承了“分解工作、传递结构化工件”的直觉，但瓶颈变了：复杂应用和主观设计任务中，问题不只是交接，还包括范围界定不足、自我评价偏差和浅层 QA。对应方案是 planner/generator/evaluator 分离、sprint contract、校准后的设计标准，以及基于 Playwright 的外部评审。Dynamic workflows 再进一步：不要求用户提前写静态 orchestration，而是让 Claude 按当前任务生成 JavaScript workflow，组合 fan-out、adversarial verification、tournament 或 loop-until-done。

Agents that remember 则把“记忆”从手写 progress file 或单次 prompt 扩展为平台资源：memory store 以文件系统形式挂载到 session，让 agent 跨 session 读写；dreaming 异步读取历史 transcripts 和 memory store，用多智能体 harness 维护长期记忆质量。

## 变化点

| 维度 | 早期长时程 harness | 后续应用开发 harness |
|---|---|---|
| 主要失败模式 | 跨会话遗忘、一次性做太多、过早宣布完成 | 范围界定不足、context anxiety、自评偏乐观、QA 太浅 |
| 智能体角色 | Initializer + coding agent | Planner + generator + evaluator |
| 核心工件 | Feature list、progress file、git history、`init.sh` | 产品规格、sprint contract、evaluator 反馈文件、QA 日志 |
| 验证方式 | 标记 feature 通过前做浏览器自动化验证 | Evaluator 用 Playwright、评分标准和契约检查做外部评估 |
| 上下文策略 | 对有 context anxiety 的模型，用 context reset + handoff | 模型能力允许时，连续会话 + 自动 compaction 即可 |
| 设计原则 | 让每轮会话可恢复、可验证、可合并 | 分离规格、生成和判断；随着模型能力提升而简化 |

## 新增阶段：dynamic workflows

| 维度 | Dynamic workflows |
|---|---|
| 主要失败模式 | Agentic laziness、self-preferential bias、goal drift，以及长任务/并行任务中的单上下文瓶颈 |
| 智能体角色 | 由 workflow 按任务 spawn classifier、worker、verifier、judge、synthesizer、router 等角色 |
| 核心工件 | JavaScript workflow、结构化子任务输出、rubric、stop condition、token budget、worktree 输出 |
| 验证方式 | Adversarial verification、deep verification、pairwise judging、loop until done |
| 上下文策略 | 多个子智能体各自拥有干净上下文窗口，workflow 负责 synthesis 和恢复 |
| 设计原则 | 复杂/高价值任务才值得额外 compute；workflow 应 task-specific，而非通用到覆盖所有边界 |

## 新增阶段：memory stores 与 dreaming

| 维度 | Managed Agents memory / dreaming |
|---|---|
| 主要失败模式 | session 隔离导致信息无法传递；长期 memory store 无界增长、重复、过时、冲突 |
| 智能体角色 | 工作 session 写入/读取 memory；dreaming orchestrator 派 subagents 整理旧 transcripts 和 memory |
| 核心工件 | Memory store、memory files、memory versions、dream job、output memory store、Console diff |
| 验证方式 | Dreaming 做 fact-check/enrich/dedupe/organize；human 可 review output store diff |
| 上下文策略 | 新 session 通过 mounted memory store 读取长期状态；dreaming 在后台整理而不是把历史塞进当前 context |
| 设计原则 | 长期 memory 必须有 scope、access、versioning、review 和 consolidation；不可信输入场景要收窄写权限 |

## 综合启发

长时程 harness 不是固定 recipe。它通常从外化记忆和任务状态开始，只在当前模型确实失败的地方增加专门角色。模型能力提升后，部分脚手架会变成开销；但可靠基线向外扩展后，团队也能尝试更复杂、更长期的 harness。Dynamic workflows 的启发是：harness 不必总是预先设计成静态系统，也可以在任务启动时由模型根据目标、验证难度和资源预算生成。Memory stores / dreaming 的启发是：长期记忆本身也需要 harness，不只是把信息存下来，还要持续治理它的范围、权限、新鲜度、重复和可审查性。

## 开放问题

- 跨会话 handoff 工件和 evaluator 反馈能否统一为一种持久项目记忆格式？
- harness 应该如何动态选择 solo、planner+generator、完整 planner+generator+evaluator 三种模式？
- 什么 benchmark 能区分 harness 本身的价值和“只是花了更多 token/时间”的效果？
- dynamic workflow 的恢复、保存和 skill 分发机制如何与团队共享 harness policy 对齐？
- memory store 与 repo/system-of-record 的边界如何设计，才能避免长期记忆和文档事实互相冲突？
