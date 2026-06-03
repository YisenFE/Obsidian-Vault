---
type: product
status: draft
created: 2026-05-29
updated: 2026-06-03
sources:
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
  - "[[wiki/sources/2026-05-28 Harness engineering for coding agent users]]"
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
  - "[[wiki/sources/2026-06-03 A harness for every task dynamic workflows in Claude Code]]"
tags:
  - llm-wiki/entity/product
  - anthropic
  - coding-agent
---
# Claude Code

## 在本 wiki 中的角色

Claude Code 是 Anthropic 的 coding-agent 产品/团队方向，与 Anthropic harness 来源有关；在 MartinFowler.com 来源中也作为写作研究使用的 GenAI 工具被提及。

## 来源支持的要点

- 早期 Anthropic 文章称 long-horizon autonomous software engineering 是多个团队的共同努力，尤其包括 code RL 和 Claude Code teams。
- 后续 Anthropic 文章称前端设计工作源自 Claude Code 仓库中的 frontend design skill 早期工作。
- Böckeler 来源称研究和写作使用了 GenAI，包括 Claude 和 Claude Code，用于从笔记中拉取想法并润色语言。
- LangChain Anatomy 文章把 Claude Code 与 Codex 一起作为模型和 harness in the loop 后训练的 agent product 例子；同时用 Terminal Bench 说明同一模型在不同 harness 下可能表现不同。

- Claude Code shorthand 来源把 Claude Code 描述为可通过 skills、commands、hooks、subagents、rules、MCPs、plugins、statusline、editor integration 和 worktrees/tmux 组合成个人 operating harness 的工具。
- 来源中的配置路径包括 `~/.claude/skills`、`~/.claude/commands`、`~/.claude/rules`、`~/.claude/agents` 和 `~/.claude.json` project disabled MCPs。
- 来源强调 context window 是 Claude Code 使用中的稀缺资源，因此应禁用未用 MCP/plugins，并按项目控制 enabled tools。
- Claude Code dynamic workflows 来源说明，Claude Code 可以执行 JavaScript workflow 来按任务动态创建 multi-agent harness，并调度 subagents、模型选择和 worktree 隔离。
- 该来源把 dynamic workflows 定位为适合复杂、高价值任务的扩展能力，不建议所有常规 coding task 都默认使用。

- [[wiki/concepts/Claude Code Operating Harness|Claude Code Operating Harness]]
- [[wiki/concepts/MCP and Plugin Context Budget|MCP and Plugin Context Budget]]
- [[wiki/concepts/Claude Code Hooks|Claude Code Hooks]]
- [[wiki/concepts/Dynamic Workflows|Dynamic Workflows]]

## 开放问题

- Claude Code 产品行为与 Anthropic 来源中讨论的 Claude Agent SDK harness 有何差异。待验证。
- Dynamic workflows、skills、subagents 和 hooks 在 Claude Code 产品内的长期边界。待验证。
