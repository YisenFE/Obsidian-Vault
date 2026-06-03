---
type: source-summary
status: ingested
created: 2026-06-03
updated: 2026-06-03
source: "[[raw/2026-06-03 A harness for every task dynamic workflows in Claude Code]]"
external_url: https://claude.com/blog/a-harness-for-every-task-dynamic-workflows-in-claude-code
author:
  - "[[wiki/entities/people/Thariq Shihipar|Thariq Shihipar]]"
  - "[[wiki/entities/people/Sid Bidasaria|Sid Bidasaria]]"
published: 2026-06-02
published_note: "Claude blog page lists June 2, 2026; raw frontmatter says 2001-06-02 and is treated as a clipping metadata error. Raw was not modified."
tags:
  - llm-wiki/source
  - claude-code
  - dynamic-workflows
  - multi-agent
  - harness-engineering
---
# A harness for every task: dynamic workflows in Claude Code

## 一句话结论

Claude Code 的 dynamic workflows（动态工作流）把 harness 从固定配置推进到“按任务现场生成”：Claude 可以编写并执行 JavaScript workflow，调度多个子智能体、选择模型和 worktree 隔离方式，用结构化多智能体流程缓解长任务中的懒惰、偏见和目标漂移。

## 来源元数据

- 原始资料：[[raw/2026-06-03 A harness for every task dynamic workflows in Claude Code]]
- 外部链接：[Claude blog — A harness for every task](https://claude.com/blog/a-harness-for-every-task-dynamic-workflows-in-claude-code)
- 作者：[[wiki/entities/people/Thariq Shihipar|Thariq Shihipar]]、[[wiki/entities/people/Sid Bidasaria|Sid Bidasaria]]
- 发表时间：2026-06-02
- 元数据注意：raw frontmatter 的 `published: 2001-06-02` 与外部页面不一致；本次在 wiki 中按来源页记录为 2026-06-02，raw 未改。

## 关键要点

1. Dynamic workflows 允许 Claude Code 为当前任务临时创建 harness，而不是只依赖默认 coding harness 或预写好的静态 orchestrator。
2. Workflow 本质上执行 JavaScript 文件，文件可调用特殊函数来 spawn 和 coordinate subagents，并可使用 JSON、Math、Array 等标准 JavaScript 能力处理数据。
3. Workflow 可以决定子智能体使用哪个模型，以及是否在独立 worktree 中运行；这把 intelligence routing（智能程度路由）和 isolation（隔离）变成 workflow 的一部分。
4. workflow 被中断后，恢复 session 时可以继续执行，使它更适合长时程、可恢复任务。
5. 文章指出默认单上下文 agent 在长时程、大规模并行、高结构化或对抗性任务中容易遇到三类失败：agentic laziness（智能体懒惰）、self-preferential bias（自我偏好偏差）、goal drift（目标漂移）。
6. Dynamic workflow 通过多个独立上下文和聚焦目标的子智能体缓解这些问题，但代价是通常消耗更多 token，更适合复杂、高价值任务。
7. 文章把常见模式归纳为 classify-and-act、fan-out-and-synthesize、adversarial verification、generate-and-filter、tournament、loop until done。
8. 典型用例包括迁移/重构、deep research、deep verification、排序、规则遵守与记忆挖掘、根因调查、大规模 triage、探索/品味判断、轻量 evals、model routing。
9. 与静态 workflow 相比，dynamic workflow 的重点是 task-specific custom harness（面向当前任务的定制支架），而不是通用流程覆盖所有边界情况。
10. 文章建议通过提示词明确 workflow pattern、使用 quick workflow 做小型对抗审查、用 token budget 限制成本，并把可复用 workflow 保存到 `~/.claude/workflows` 或通过 skill 分发。

## 术语说明

- Dynamic Workflows（动态工作流）：Claude Code 中由 Claude 现场生成/执行的 JavaScript 多智能体工作流，用于为当前任务构造临时 harness。
- Task-specific Harness（面向任务的定制支架）：不是通用固定流程，而是围绕当前任务的结构、风险、验证方式和资源约束动态组织的 harness。
- Agentic Laziness（智能体懒惰）：智能体在复杂多部分任务中提前停下并宣称完成的失败模式。
- Self-preferential Bias（自我偏好偏差）：智能体更倾向相信自己生成的结论，尤其在验证或评分自己输出时。
- Goal Drift（目标漂移）：长任务或 compaction 后，原始目标和负约束逐步丢失或弱化。
- Fan-out-and-synthesize（分发并综合）：把任务拆成多个独立子任务并行处理，再在 barrier step 合并结构化结果。
- Tournament（锦标赛式比较）：多个子智能体用不同方案完成同一任务，再由 judge agent 逐轮比较筛选。
- Quarantine（隔离区）：让读取不可信内容的智能体不能执行高权限动作，由另一个可信执行角色处理行动。

## 需要更新的概念

- [[wiki/concepts/Dynamic Workflows|Dynamic Workflows]]
- [[wiki/concepts/Long-running Agent Failure Modes|Long-running Agent Failure Modes]]
- [[wiki/concepts/Claude Code Operating Harness|Claude Code Operating Harness]]
- [[wiki/concepts/Parallel Agent Workflows|Parallel Agent Workflows]]
- [[wiki/concepts/Subagent Scoping|Subagent Scoping]]
- [[wiki/concepts/External Evaluator Agent|External Evaluator Agent]]
- [[wiki/concepts/Self-verification|Self-verification]]
- [[wiki/concepts/Agent Rules and Memory|Agent Rules and Memory]]
- [[wiki/concepts/Context Reset vs Compaction|Context Reset vs Compaction]]
- [[wiki/concepts/Harness Engineering|Harness Engineering]]

## 需要更新的实体

- 人物：[[wiki/entities/people/Thariq Shihipar|Thariq Shihipar]]、[[wiki/entities/people/Sid Bidasaria|Sid Bidasaria]]
- 组织：[[wiki/entities/organizations/Anthropic|Anthropic]]
- 产品/工具：[[wiki/entities/products/Claude Code|Claude Code]]、[[wiki/entities/products/Claude Agent SDK|Claude Agent SDK]]、[[wiki/entities/products/Claude Opus 4.8|Claude Opus 4.8]]、[[wiki/entities/products/Bun|Bun]]

## 论断 / 证据

| 论断 | 证据 | 置信度 |
|---|---|---:|
| Dynamic workflows 让 Claude Code 能按任务生成自己的 harness。 | 文章开头说明 Claude Code 可以 on the fly 编写并编排多智能体 harness，并把 workflow 描述为 built on top of Claude Code 的动态 harness。 | 高：来源直接陈述 |
| 单上下文默认 harness 在长时程、并行、结构化或对抗性任务中容易失效。 | 文章列出 agentic laziness、self-preferential bias、goal drift 三类失败，并解释 compaction 后细节可能丢失。 | 高：来源支持 |
| 多子智能体和独立上下文可以结构性缓解自评偏差和目标漂移。 | 文章称 workflow 通过 focused, isolated goals 的子智能体与独立 context windows 对抗这些失败模式。 | 中高：来源机制解释，仍需外部验证 |
| Dynamic workflows 更适合复杂、高价值任务，不应成为所有任务默认选择。 | 文章明确提醒 best practices 仍在发展，workflow 往往用更多 token，常规 coding task 不一定需要更多 compute。 | 高：来源直接注意事项 |
| workflow pattern 可以组合成迁移、研究、验证、排序、triage、evals、模型路由等任务 harness。 | 来源逐项列出模式和用例，并给出 prompt 示例。 | 高：来源直接列举 |

## 冲突 / 注意事项

- Raw frontmatter 的 `published: 2001-06-02` 很可能是剪藏元数据错误；外部 Claude blog 页面显示日期为 2026-06-02。本次未修改 raw，只在 wiki 记录差异。
- 来源是官方产品文章和经验总结，不是 controlled benchmark；workflow 质量、成本和 token 使用需要在具体任务中验证。
- 文中提到 Claude Opus 4.8、dynamic workflows、`ultracode`、`/loop`、workflow menu、`~/.claude/workflows` 等产品能力均是来源时间点陈述，可能随 Claude Code 版本变化。
- Bun 从 Zig 到 Rust 的迁移案例来自文章引用的 X thread；本次未独立核验该迁移细节。
- 外部图示未下载到 `raw/assets/`；本次依据文本内容和来源页元数据完成 ingest。

## 后续问题

- Dynamic workflows 与已有 skills/subagents/hooks 的边界是什么：什么时候保存为 workflow，什么时候封装为 skill，什么时候只写一次性 prompt？
- workflow 的 token budget、并行度和 worktree 数量应如何系统调参？
- 对抗验证 agent 如何避免制造过多 false positives？
- 读取不可信内容的 triage workflow 如何实现 quarantine 和权限隔离？
- Dynamic workflow 能否作为 [[wiki/concepts/Natural-Language Agent Harnesses|NLAH]] 或 `AGENTS.md` 这类自然语言 policy 的执行载体？
