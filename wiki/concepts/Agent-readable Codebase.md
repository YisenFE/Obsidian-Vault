---
type: concept
status: draft
created: 2026-05-28
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 工程技术：在智能体优先的世界中利用 Codex]]"
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
  - "[[wiki/sources/2026-05-28 Harness engineering for coding agent users]]"
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
tags:
  - llm-wiki/concept
  - agent-readability
---
# Agent-readable Codebase

## 定义

智能体可读代码库（Agent-readable Codebase）是一种面向智能体可导航性优化的代码库：关键业务知识、运行信号、工具入口、约束、交接记录、guides、sensors 和验证路径都以智能体可发现、可查询、可执行的形式存在于本地或标准工具中。

## 为什么重要

对智能体来说，运行时无法进入上下文或被工具访问的信息几乎等同于不存在。把知识留在聊天记录、会议、Google Docs 或个人脑中，会让智能体像缺失背景的新员工一样行动；把知识版本化并暴露给工具，则能提高一致性和自治程度。

## 来源支持的要点

- OpenAI 文章强调为 Codex 的可读性优化代码库，就像团队会为新人优化代码可导航性。
- 应用可按 git worktree 启动，使 Codex 能为每次变更驱动独立实例。
- [[wiki/entities/products/Chrome DevTools MCP|Chrome DevTools MCP]]、DOM 快照、截图和导航技能让 Codex 能观察 UI 行为并验证修复。
- 本地可观测性栈让 Codex 使用 LogQL、PromQL、TraceQL 查询日志、指标和 trace，并把信号用于修复/重启/重跑循环。
- Anthropic 来源中的 `claude-progress.txt`、git history、feature list 和 `init.sh` 是 agent-readable codebase 的长时程版本。
- Böckeler 来源把 LSP、architecture.md、AGENTS.md、/how-to-test skill、API docs、CLI/scripts、codemods、logs 和 browser 都放进 user harness 的 guides/sensors 体系。
- 这说明“agent-readable”不只是文档结构，也包括 deterministic tooling 和 inferential review tools 是否能进入 agent loop。

- Michael Bolin 访谈强调，agent-first world 让文档、测试驱动开发、清晰命名和严格架构这些旧 best practices 重新变得明显值得。
- Codex 团队倾向 modest `AGENTS.md`：记录 agent 难以从代码快速发现的信息，例如测试运行方式和测试优先级，而不是复制源码中的知识。
- 文件/文件夹命名、仓库结构和 PR/GitHub context 也是 agent-readable codebase 的组成部分，因为 Codex 会主动 grep/read code 并根据已有模式行动。

- Claude Code shorthand 来源提出 codemap-updater skill：在 checkpoint 生成/更新代码地图，帮助 Claude 快速导航代码库而不重复消耗上下文探索。
- LSP plugins、editor file watchers、autosave、git integration 和 `@` 文件搜索也让代码库对 agent/用户更可读。

## 相关概念

- [[wiki/concepts/Context Engineering for Coding Agents|Context Engineering for Coding Agents]]
- [[wiki/concepts/Small Powerful Tool Surface|Small Powerful Tool Surface]]

- [[wiki/concepts/Repository as System of Record|Repository as System of Record]]
- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Feedforward Guides|Feedforward Guides]]
- [[wiki/concepts/Feedback Sensors|Feedback Sensors]]
- [[wiki/concepts/Harnessability|Harnessability]]
- [[wiki/concepts/Mechanized Invariants|Mechanized Invariants]]

- 如何在 modest `AGENTS.md` 与更完整的 docs-as-system-of-record 之间分层？

- [[wiki/concepts/Codemaps for Agents|Codemaps for Agents]]

## 开放问题

- 哪些信息必须进入仓库，哪些可以留在外部知识系统但通过工具暴露？
- 可读性优化是否会与人类偏好的抽象/复用发生冲突？
- 如何衡量一个代码库对智能体“可读”？
- Agent-readable 与 harnessability 的区别和重叠如何定义？
