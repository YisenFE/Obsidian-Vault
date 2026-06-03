---
type: concept
status: draft
created: 2026-06-01
updated: 2026-06-01
aliases:
  - Rules folder
  - CLAUDE.md memory
sources:
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
tags:
  - llm-wiki/concept
  - memory
  - rules
  - claude-code
---
# Agent Rules and Memory

## 定义

Agent Rules and Memory（智能体规则与记忆）是把 agent 应长期遵守的项目/个人偏好写入 `CLAUDE.md`、`AGENTS.md` 或模块化 rules folder 的做法。它不同于当前任务 prompt，更像长期可复用的 feedforward guide。

## 为什么重要

许多偏好不该每次重复写在 prompt 里，例如安全要求、代码风格、测试策略、git workflow、subagent delegation 和性能策略。规则/记忆层让这些约束稳定进入 agent 行为，但也要避免过长、过旧或与代码冲突。

## 来源支持的要点

- Claude Code shorthand 来源给出两种做法：单个 `CLAUDE.md`，或 `~/.claude/rules/*.md` 按 concern 模块化。
- 示例 rules 包括 security、coding-style、testing、git-workflow、agents、patterns、performance、hooks。
- 具体偏好包括不写硬编码 secrets、先测试、模块化、禁止不必要的 `console.log`、前端避免某些颜色等。
- Bolin 访谈则提醒 `AGENTS.md` 应保持 modest，只记录 agent 不容易从代码推断的信息。

## 相关概念

- [[wiki/concepts/Feedforward Guides|Feedforward Guides]]
- [[wiki/concepts/Agent-readable Codebase|Agent-readable Codebase]]
- [[wiki/concepts/Context Engineering for Coding Agents|Context Engineering for Coding Agents]]
- [[wiki/concepts/Coding Agent User Harness|Coding Agent User Harness]]

## 开放问题

- 个人 rules 与项目 rules 冲突时，优先级如何定义？
- Rules 过多时如何避免 context rot？
- 哪些长期偏好应该升级为 hook/lint/test，而不是停留在自然语言？
