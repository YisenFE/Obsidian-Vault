---
type: source-summary
status: ingested
created: 2026-06-01
updated: 2026-06-01
source: "[[raw/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
external_url: https://x.com/affaan/status/2012378465664745795
author: "[[wiki/entities/people/affaan|@affaan]]"
published: 2026-01-17
published_corrected: 2026-06-01
published_note: "Corrected raw frontmatter from 2025-09-16 to 2026-01-17 on 2026-06-01; 2025-09-16 is retained in the body as quoted hackathon post date."
image_assets:
  - "[[raw/assets/2026-06-01-claude-code-shorthand-01-hero-setup.jpg]]"
  - "[[raw/assets/2026-06-01-claude-code-shorthand-02-command-chaining.jpg]]"
  - "[[raw/assets/2026-06-01-claude-code-shorthand-03-posttooluse-hook-feedback.png]]"
  - "[[raw/assets/2026-06-01-claude-code-shorthand-04-supabase-mcp-tables.jpg]]"
  - "[[raw/assets/2026-06-01-claude-code-shorthand-05-plugins-mcp-status.jpg]]"
  - "[[raw/assets/2026-06-01-claude-code-shorthand-06-mixedbread-grep-marketplace.jpg]]"
  - "[[raw/assets/2026-06-01-claude-code-shorthand-07-tmux-video-poster.jpg]]"
  - "[[raw/assets/2026-06-01-claude-code-shorthand-08-github-actions-pr-review.jpg]]"
  - "[[raw/assets/2026-06-01-claude-code-shorthand-09-zed-command-palette.jpg]]"
  - "[[raw/assets/2026-06-01-claude-code-shorthand-10-vscode-extension-docs.jpg]]"
  - "[[raw/assets/2026-06-01-claude-code-shorthand-11-custom-statusline.jpg]]"
tags:
  - llm-wiki/source
  - claude-code
  - user-harness
  - context-management
  - coding-agents
---
# The Shorthand Guide to Everything Claude Code

## 一句话结论

这篇 X 线程把 [[wiki/entities/products/Claude Code|Claude Code]] 的高效日常使用整理成一套用户侧 operating harness：用 skills/commands 复用工作流，用 hooks 自动注入检查和反馈，用 subagents 限定任务边界，用 rules/memory 固化偏好，用 MCPs/plugins 扩展能力，同时严格控制工具数量、上下文窗口和并行工作隔离。

## 来源元数据

- 原始资料：[[raw/2026-06-01 The Shorthand Guide to Everything Claude Code]]
- 外部链接：[X — @affaan status 2012378465664745795](https://x.com/affaan/status/2012378465664745795)
- 作者：[[wiki/entities/people/affaan|@affaan]]
- 发布时间：2026-01-17（已按 X snowflake id 推断结果修正 raw frontmatter；正文中的 2025-09-16 保留为被引用 hackathon 帖日期）
- 本地图片资产（ingest 时已下载并查看）：
  - 01-hero-setup: [[raw/assets/2026-06-01-claude-code-shorthand-01-hero-setup.jpg]]
  - 02-command-chaining: [[raw/assets/2026-06-01-claude-code-shorthand-02-command-chaining.jpg]]
  - 03-posttooluse-hook-feedback: [[raw/assets/2026-06-01-claude-code-shorthand-03-posttooluse-hook-feedback.png]]
  - 04-supabase-mcp-tables: [[raw/assets/2026-06-01-claude-code-shorthand-04-supabase-mcp-tables.jpg]]
  - 05-plugins-mcp-status: [[raw/assets/2026-06-01-claude-code-shorthand-05-plugins-mcp-status.jpg]]
  - 06-mixedbread-grep-marketplace: [[raw/assets/2026-06-01-claude-code-shorthand-06-mixedbread-grep-marketplace.jpg]]
  - 07-tmux-video-poster: [[raw/assets/2026-06-01-claude-code-shorthand-07-tmux-video-poster.jpg]]
  - 08-github-actions-pr-review: [[raw/assets/2026-06-01-claude-code-shorthand-08-github-actions-pr-review.jpg]]
  - 09-zed-command-palette: [[raw/assets/2026-06-01-claude-code-shorthand-09-zed-command-palette.jpg]]
  - 10-vscode-extension-docs: [[raw/assets/2026-06-01-claude-code-shorthand-10-vscode-extension-docs.jpg]]
  - 11-custom-statusline: [[raw/assets/2026-06-01-claude-code-shorthand-11-custom-statusline.jpg]]

## 关键要点

1. 文章把 Claude Code 的个人配置分为 skills/commands、hooks、subagents、rules/memory、MCPs、plugins、parallel workflows、editor integration 与 statusline 等层。
2. [[wiki/concepts/Skills as Progressive Disclosure|Skills]] 被用作 workflow shorthand：例如 `/refactor-clean`、`/tdd`、`/e2e`、`/test-coverage`，可在单次 prompt 中串联；skills 放在 `~/.claude/skills`，commands 放在 `~/.claude/commands`。
3. Codemap updater 这类 skill 可以在 checkpoint 更新代码地图，让 Claude 快速导航代码库，减少上下文花在重复探索上。
4. [[wiki/concepts/Claude Code Hooks|Hooks]] 是基于工具调用和生命周期事件的自动化：PreToolUse、PostToolUse、UserPromptSubmit、Stop、PreCompact、Notification。
5. Hook 示例包括：长命令前提醒使用 tmux、编辑后自动 Prettier、TypeScript 检查、发现 `console.log` 警告、push 前打开编辑器 review、session 结束前审计修改文件。
6. [[wiki/concepts/Subagent Scoping|Subagents]] 是主 Claude 可委派的有限范围执行进程；作者建议按 planner、architect、tdd-guide、code-reviewer、security-reviewer、e2e-runner、refactor-cleaner、doc-updater 等角色拆分，并配置允许工具/MCP/权限。
7. Rules/memory 层可用单个 `CLAUDE.md` 或 `~/.claude/rules/*.md` 模块化表达长期偏好，例如安全、编码风格、测试、git workflow、delegation、performance、hooks。
8. MCPs（[[wiki/entities/products/Model Context Protocol|Model Context Protocol]] servers）连接外部服务，如 Supabase、GitHub、Vercel、Railway、Cloudflare、ClickHouse、Firecrawl 等；作者强调 MCP 不是 API 替代品，而是 prompt-driven wrapper。
9. 文章最强的上下文管理建议是：MCP/plugin 要配置和启用分离；可以配置 20-30 个 MCP，但每个项目只启用少量，作者经验是低于 10 个 MCP / 80 个 tools。
10. Plugins 用于打包 skills、MCP、hooks 或 tools，降低安装成本；示例包括 LSP plugins、hookify、mgrep、frontend-design、commit-commands、security-guidance、pr-review-toolkit。
11. LSP plugins 对离开 IDE 使用 Claude Code 的场景特别有用，可以给 agent 提供类型检查、go-to-definition 等代码智能。
12. 并行工作有两个层次：`/fork` 适合非重叠任务；git worktrees 适合会改同一 repo 的并行 Claude，避免工作区冲突。
13. tmux 用于长命令和服务日志：让 Claude 启动 frontend/backend server 后，用户可以 detach/attach 观察日志和维持 session。
14. 作者建议用 sandbox mode 处理风险操作，并明确提醒 `--dangerously-skip-permissions` 会让 Claude 大范围行动，可能破坏系统。
15. Editor integration 是用户侧 harness 的一部分：[[wiki/entities/products/Zed|Zed]]、[[wiki/entities/products/VS Code|VS Code]] / Cursor 能提供实时文件跟踪、命令面板、LSP、git review、autosave 和文件 watcher。
16. 自定义 statusline 显示用户、目录、git branch、dirty 状态、context 剩余比例、model、时间和 todo 数，是一种运行时可观测性小面板。
17. 最后五条原则是：不要过度复杂化；context window 是稀缺资源；并行执行要隔离；重复动作自动化；subagent 要有限工具、聚焦执行。

## 术语说明

- Skills/Commands（技能/斜杠命令）：可复用 prompt/workflow shorthand；skills 偏广义流程，commands 偏快速执行入口。
- Hooks（事件钩子）：在工具调用前后、用户提交、停止、压缩前、权限通知等事件触发的自动化。
- Subagents（子智能体）：由主 Claude 委派、带有限上下文/工具/权限的专门角色。
- MCPs（Model Context Protocol servers，模型上下文协议服务器）：把外部服务包装成 agent 可调用能力的协议/服务器。
- Plugins（插件）：把 skills、MCP、hooks 或 tools 打包成可安装单元。
- Tool budget（工具预算）：在上下文窗口内可承受的启用工具/MCP/plugin 数量。
- Worktree（Git 工作树）：同一 repo 的独立 checkout，用于并行 agent 工作隔离。

## 需要更新的概念

- [[wiki/concepts/Claude Code Operating Harness|Claude Code Operating Harness]]
- [[wiki/concepts/Claude Code Hooks|Claude Code Hooks]]
- [[wiki/concepts/Subagent Scoping|Subagent Scoping]]
- [[wiki/concepts/MCP and Plugin Context Budget|MCP and Plugin Context Budget]]
- [[wiki/concepts/Parallel Agent Workflows|Parallel Agent Workflows]]
- [[wiki/concepts/Agent Rules and Memory|Agent Rules and Memory]]
- [[wiki/concepts/Codemaps for Agents|Codemaps for Agents]]
- [[wiki/concepts/Coding Agent User Harness|Coding Agent User Harness]]
- [[wiki/concepts/Skills as Progressive Disclosure|Skills as Progressive Disclosure]]
- [[wiki/concepts/Middleware Hooks|Middleware Hooks]]
- [[wiki/concepts/Context Rot|Context Rot]]
- [[wiki/concepts/Feedforward Guides|Feedforward Guides]]
- [[wiki/concepts/Feedback Sensors|Feedback Sensors]]
- [[wiki/concepts/Mechanized Invariants|Mechanized Invariants]]
- [[wiki/concepts/Agent-readable Codebase|Agent-readable Codebase]]

## 需要更新的实体

- 人物：[[wiki/entities/people/affaan|@affaan]]
- 组织：[[wiki/entities/organizations/Anthropic|Anthropic]]
- 产品/工具：[[wiki/entities/products/Claude Code|Claude Code]]、[[wiki/entities/products/Model Context Protocol|Model Context Protocol]]、[[wiki/entities/products/Zed|Zed]]、[[wiki/entities/products/VS Code|VS Code]]、[[wiki/entities/products/Cursor|Cursor]]、[[wiki/entities/products/tmux|tmux]]、[[wiki/entities/products/mgrep|mgrep]]、[[wiki/entities/products/hookify|hookify]]、[[wiki/entities/products/Supabase|Supabase]]、[[wiki/entities/products/GitHub Actions|GitHub Actions]]

## 论断 / 证据

| 论断 | 证据 | 置信度 |
|---|---|---:|
| Claude Code 的高效使用依赖多层用户侧 harness，而不是单个提示词。 | 文章系统列出 skills、hooks、subagents、rules、MCPs、plugins、editor、worktrees、tmux、statusline。 | 高：来源直接陈述 |
| MCP/plugin 数量会显著影响 context window 和性能。 | 作者称 200k 窗口在过多 tools enabled 时可能只剩 70k，并给出低于 10 MCP / 80 tools 的经验规则。 | 中：个人经验，需验证 |
| Hooks 可以把重复检查转成自动反馈。 | Hook 示例覆盖 PreToolUse、PostToolUse、Stop，执行 tmux reminder、format、tsc、console.log warning、push review。 | 高：来源示例支持 |
| Subagents 应按角色和权限收窄。 | 作者列出 planner、architect、security-reviewer、e2e-runner 等，并建议配置 allowed tools/MCPs/permissions。 | 高：来源支持的实践 |
| 并行 Claude 工作需要隔离机制。 | 来源建议 `/fork` 用于非重叠任务，git worktrees 用于重叠并行 Claude。 | 高：来源支持的实践 |
| Editor integration 可成为 Claude Code harness 的观察面。 | 来源说明 Zed/VS Code/Cursor 可提供文件跟踪、跳转、命令面板、LSP、git review、autosave。 | 中高：来源经验判断 |

## 冲突 / 注意事项

- Raw frontmatter 已从 `published: 2025-09-16` 修正为 `published: 2026-01-17`；正文内 2025-09-16 是被引用 hackathon 帖日期，保留不改。
- 该来源是个人经验线程，不是系统 benchmark；“低于 10 MCP / 80 tools”“200k 变 70k”等数字应视为经验规则。
- 文中出现的 Claude Code 版本、Opus 4.5、plugin marketplace、MCP server 状态和编辑器集成能力均是来源时间点陈述，可能变化。
- `--dangerously-skip-permissions` 明确带破坏风险；本 wiki 只记录来源提及，不建议默认使用。
- 图片与视频截图主要支持界面/设置示例；视频 blob 未下载，仅保存了 poster 图。

## 后续问题

- 个人/团队 Claude Code harness 的最小配置应包含哪些：rules、skills、hooks、subagents、MCP budget、statusline，还是 worktree/tmux？
- MCP/tool budget 应如何量化：看 tool 数、tokens、latency，还是任务失败率？
- 哪些 hooks 应该进入项目仓库，哪些应留在个人 `~/.claude` 配置？
- Subagent 与 skill 的边界在哪里：什么时候封装 skill，什么时候拆成 subagent？
- 是否需要把本 vault 的 AGENTS/wiki 维护流程也抽象成 Claude Code skill 或 hook？
