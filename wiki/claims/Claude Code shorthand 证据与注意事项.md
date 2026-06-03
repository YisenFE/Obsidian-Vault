---
type: claim-set
status: draft
created: 2026-06-01
updated: 2026-06-01
aliases:
  - Claude Code shorthand evidence and caveats
sources:
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
tags:
  - llm-wiki/claim
  - claude-code
  - user-harness
---
# Claude Code shorthand 证据与注意事项

## 范围

本页追踪 @affaan 关于 Claude Code 日常配置的主要实践论断：skills/commands、hooks、subagents、rules/memory、MCP/plugin context budget、parallel workflows、editor integration、sandboxing 与 CI review。

## 来源支持的论断

| 论断 | 来源证据 | 状态 |
|---|---|---|
| Claude Code user harness 可由 skills、hooks、subagents、rules、MCPs、plugins 等分层组成。 | 来源逐段给出目录结构、hook JSON、subagent 列表、rules folder、MCP config、plugins 列表。 | 来源支持 |
| Skills/commands 适合把重复工作流短语化。 | 来源例子包括 `/refactor-clean`、`/tdd`、`/e2e`、`/test-coverage`，并展示命令串联。 | 来源支持 |
| Hooks 能把格式化、类型检查、日志警告、tmux 提醒等转成自动反馈。 | 来源列出 PreToolUse、PostToolUse、Stop 示例。 | 来源支持 |
| MCP/plugin 需要预算管理。 | 作者称启用太多工具会显著压缩上下文，并给出 <10 MCP / <80 tools 的经验规则。 | 个人经验，待验证 |
| Subagents 应按职责和权限限定。 | 来源列出 planner、architect、tdd-guide、reviewer、e2e-runner 等，并建议配置 allowed tools/MCPs/permissions。 | 来源支持 |
| 并行工作需要 `/fork`、git worktrees、tmux 等隔离/观察机制。 | 来源分别给出 `/fork`、git worktree 和 tmux 示例。 | 来源支持 |
| Sandbox mode 应用于风险操作，skip permissions 有破坏风险。 | 来源明确警告 `--dangerously-skip-permissions` 可能破坏系统。 | 来源支持 |

## 注意事项 / 局限

- 这是个人经验线程，不是官方文档或 controlled study。
- raw frontmatter 已按 X status id 推断日期修正为 `published: 2026-01-17`；正文中 2025-09-16 仍作为被引用 hackathon 帖日期保留。
- 文中 Claude Code 版本、Opus 4.5、plugin marketplace 和 MCP/tool 状态可能随时间变化。
- MCP/tool 数量规则是作者经验；不同模型、任务和工具描述长度下可能不适用。
- 文中提到许多 third-party MCP/plugin/server；本 wiki 未审计其安全性、权限范围或供应链风险。

## 后续待验证问题

| 问题 | 为什么重要 | 状态 |
|---|---|---|
| <10 MCP / <80 tools 是否是可泛化预算？ | 影响团队级 Claude Code 配置默认值。 | 待验证 |
| Hooks 是放在个人 config 还是 repo config 更安全？ | 影响可复现性和误伤风险。 | 待验证 |
| Subagent 权限边界如何最小化？ | 关系到多 agent 安全和上下文污染。 | 待验证 |
| Codemap updater 是否真的降低探索成本？ | 需要用 trace/token/latency 证据验证。 | 待验证 |
| raw published 元数据是否应修正？ | 影响来源时间线。 | 已于 2026-06-01 修正为 2026-01-17 |

## 相关页面

- [[wiki/concepts/Claude Code Operating Harness|Claude Code Operating Harness]]
- [[wiki/concepts/Claude Code Hooks|Claude Code Hooks]]
- [[wiki/concepts/Subagent Scoping|Subagent Scoping]]
- [[wiki/concepts/MCP and Plugin Context Budget|MCP and Plugin Context Budget]]
- [[wiki/concepts/Parallel Agent Workflows|Parallel Agent Workflows]]
