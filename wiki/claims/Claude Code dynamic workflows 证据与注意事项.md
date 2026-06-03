---
type: claim-set
status: draft
created: 2026-06-03
updated: 2026-06-03
aliases:
  - Claude Code dynamic workflows evidence and caveats
sources:
  - "[[wiki/sources/2026-06-03 A harness for every task dynamic workflows in Claude Code]]"
tags:
  - llm-wiki/claim
  - claude-code
  - dynamic-workflows
  - multi-agent
---
# Claude Code dynamic workflows 证据与注意事项

## 范围

本页追踪 Anthropic / Claude blog 对 Claude Code dynamic workflows 的主要论断：按任务生成 harness、JavaScript workflow 编排子智能体、常见 workflow patterns、适用场景、成本边界和未验证案例。

## 来源支持的论断

| 论断 | 来源证据 | 状态 |
|---|---|---|
| Claude Code 可以按任务动态创建多智能体 harness。 | 文章称 Claude 可以 on the fly 编写和编排自己的 multi-agent harness，workflow built on top of Claude Code。 | 来源支持 |
| Dynamic workflow 执行 JavaScript 文件并可协调 subagents。 | 文章说明 workflow 执行带特殊函数的 JavaScript 文件，并可使用 JSON、Math、Array 等标准函数。 | 来源支持 |
| workflow 可以选择模型和 worktree 隔离方式。 | 文章称 workflow 可决定 agent 使用哪个模型，以及 subagents 是否在自己的 worktree 中运行。 | 来源支持 |
| Dynamic workflow 主要缓解单上下文长任务中的懒惰、自我偏好和目标漂移。 | 文章在 “Why dynamic workflows” 中列出 agentic laziness、self-preferential bias、goal drift，并说明多子智能体独立上下文如何缓解。 | 来源支持，机制仍待实证 |
| 常见 workflow patterns 包括分类路由、分发综合、对抗验证、生成筛选、锦标赛、循环直到完成。 | 来源逐项定义这些模式，并给出迁移、研究、验证、排序、triage、evals 等用例。 | 来源支持 |
| Dynamic workflows 不适合所有任务。 | 来源提示 best practices 仍在发展，workflow 通常更耗 token，常规 coding task 不一定需要更多 compute。 | 来源支持 |

## 注意事项 / 局限

- 官方文章提供的是产品能力说明和实践建议，不是 benchmark；“更适合复杂高价值任务”的判断需要按任务成本和质量验证。
- Bun 重写案例来自文章引用的外部 X thread，本 wiki 当前未独立核验。
- Claude Opus 4.8、`ultracode`、workflow menu、`/loop`、`~/.claude/workflows` 等产品行为可能随 Claude Code 版本变化。
- raw frontmatter 的 `published: 2001-06-02` 与外部页面的 2026-06-02 不一致；本页按外部来源记录，raw 未改。
- 对抗验证和 tournament 可能增加 token、延迟和 false positives；不是所有任务都值得使用。

## 后续待验证问题

| 问题 | 为什么重要 | 状态 |
|---|---|---|
| dynamic workflow 相比静态 workflow / 单 agent 的质量提升能否量化？ | 决定团队是否应默认使用 workflow。 | 待验证 |
| token budget 与并行度如何影响结果质量？ | 直接关系成本和延迟。 | 待验证 |
| workflow 的恢复语义能否跨中断稳定保持？ | 影响长时程可靠性。 | 待验证 |
| quarantine pattern 在 Claude Code 权限模型中如何具体实现？ | 关系到处理不可信输入的安全边界。 | 待验证 |
| workflow 与 skill 的复用边界在哪里？ | 影响团队沉淀 workflow 的方式。 | 待验证 |

## 相关页面

- [[wiki/concepts/Dynamic Workflows|Dynamic Workflows]]
- [[wiki/concepts/Long-running Agent Failure Modes|Long-running Agent Failure Modes]]
- [[wiki/concepts/Claude Code Operating Harness|Claude Code Operating Harness]]
- [[wiki/concepts/Parallel Agent Workflows|Parallel Agent Workflows]]
- [[wiki/concepts/Subagent Scoping|Subagent Scoping]]
