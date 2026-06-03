---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
aliases:
  - Skills
  - Progressive disclosure
sources:
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
  - "[[wiki/sources/2026-05-28 Harness engineering for coding agent users]]"
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
tags:
  - llm-wiki/concept
  - skills
  - context-management
  - feedforward-guides
---
# Skills as Progressive Disclosure

## 定义

Skills as Progressive Disclosure（技能作为渐进披露）是指 harness 只在 agent 启动时暴露技能的轻量 frontmatter / 摘要，等任务需要时再加载完整说明、脚本或模板，以避免把大量工具说明一次性塞入上下文。

## 为什么重要

技能可以把重复流程、工具用法和团队经验封装成 agent 可调用知识；但技能过多会在启动时污染上下文。渐进披露让 agent 先知道“有什么能力”，再按需读取“怎么做”。

## 来源支持的要点

- LangChain Anatomy 文章把 skills 列为对抗 context rot 的 harness primitive，因为过多 tools/MCP servers 启动加载会降低性能。
- Böckeler 来源把 skills 放在用户侧 feedforward guides 中：团队可以通过 skills 引导 agent 执行常见流程。
- Bolin 访谈中也提到开发者可以把重复做法沉淀成 skill，并分享给队友。

- Claude Code shorthand 来源补充了具体落点：skills 放在 `~/.claude/skills`，commands 放在 `~/.claude/commands`；commands 是通过斜杠命令快速执行的 skill-like prompt。
- `/refactor-clean`、`/tdd`、`/e2e`、`/test-coverage` 这类命令可串联，形成短语化 workflow。
- `codemap-updater` 这类 skill 可以在 checkpoint 更新代码地图，减少 agent 反复探索代码库造成的上下文消耗。

## 相关概念

- [[wiki/concepts/Feedforward Guides|Feedforward Guides]]
- [[wiki/concepts/Context Rot|Context Rot]]
- [[wiki/concepts/Context Engineering for Coding Agents|Context Engineering for Coding Agents]]
- [[wiki/concepts/Coding Agent User Harness|Coding Agent User Harness]]

- [[wiki/concepts/Codemaps for Agents|Codemaps for Agents]]
- [[wiki/concepts/Claude Code Operating Harness|Claude Code Operating Harness]]

## 开放问题

- Skill frontmatter 应包含哪些字段，既能被检索又不造成上下文噪声？
- 技能何时应封装脚本，何时只保留文字流程？
- 如何避免过期技能误导 agent？
