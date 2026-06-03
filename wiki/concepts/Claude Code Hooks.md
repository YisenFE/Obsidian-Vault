---
type: concept
status: draft
created: 2026-06-01
updated: 2026-06-01
aliases:
  - Claude hooks
  - Hook automation
sources:
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
tags:
  - llm-wiki/concept
  - hooks
  - claude-code
  - feedback-sensors
---
# Claude Code Hooks

## 定义

Claude Code Hooks（Claude Code 事件钩子）是在 Claude Code 工具调用或生命周期事件上触发的自动化机制。它们可以在工具执行前提醒/阻断，在工具执行后格式化/检查，在会话停止前审计结果，或在压缩/权限事件中插入反馈。

## 为什么重要

Hooks 把“人类每次都要提醒 agent 的事”变成确定性控制点。例如长命令前提醒 tmux、编辑后运行格式化和类型检查、push 前要求 review、停止前检查 `console.log`。这使 user harness 从自然语言 guide 升级为可执行 feedback sensor。

## 来源支持的要点

- 来源列出 Hook Types：PreToolUse、PostToolUse、UserPromptSubmit、Stop、PreCompact、Notification。
- PreToolUse 示例：对 `npm`、`pnpm`、`yarn`、`cargo`、`pytest` 等长命令提醒使用 tmux。
- PostToolUse 示例：编辑 JS/TS 后运行 Prettier，编辑 TS 后运行 `tsc --noEmit`，扫描 `console.log`。
- Stop hook 示例：session 结束前审计修改文件中的 `console.log`。
- 来源建议使用 `hookify` plugin conversationally 创建 hooks，而不是手写 JSON。

## 相关概念

- [[wiki/concepts/Middleware Hooks|Middleware Hooks]]
- [[wiki/concepts/Feedback Sensors|Feedback Sensors]]
- [[wiki/concepts/Mechanized Invariants|Mechanized Invariants]]
- [[wiki/concepts/Self-verification|Self-verification]]
- [[wiki/entities/products/hookify|hookify]]

## 开放问题

- 哪些 hook 应默认阻断，哪些只应提示？
- Hook 失败时应阻断 agent，还是只记录警告？
- 团队共享 hooks 如何避免误伤不同项目和语言栈？
