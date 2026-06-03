---
type: concept
status: draft
created: 2026-06-01
updated: 2026-06-01
aliases:
  - Codemap
  - Code maps for agents
sources:
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
tags:
  - llm-wiki/concept
  - agent-readable-codebase
  - context-engineering
---
# Codemaps for Agents

## 定义

Codemaps for Agents（面向智能体的代码地图）是在 checkpoint 或重要变更后生成/更新的代码库导航文件，帮助 agent 快速理解目录、模块、关键入口和变更位置，减少重复 grep/read 探索。

## 为什么重要

Agent 需要搜索代码库，但每次从零探索会消耗上下文和时间。Codemap 把“哪里有什么”变成可读索引；如果能自动更新，它就成为 agent-readable codebase 的一部分。

## 来源支持的要点

- Claude Code shorthand 来源提到可做 `codemap-updater` skill，在 checkpoints 更新 codemaps，让 Claude 快速导航代码库而不浪费上下文。
- Bolin 访谈强调文件/文件夹命名和仓库结构会影响 Codex 自行搜索代码库的效率；codemap 是这一思想的显式化。

## 相关概念

- [[wiki/concepts/Agent-readable Codebase|Agent-readable Codebase]]
- [[wiki/concepts/Context Engineering for Coding Agents|Context Engineering for Coding Agents]]
- [[wiki/concepts/Skills as Progressive Disclosure|Skills as Progressive Disclosure]]
- [[wiki/concepts/Repository as System of Record|Repository as System of Record]]

## 开放问题

- Codemap 应由 agent 更新、hook 更新，还是 CI 更新？
- Codemap 如何检测过期并避免误导 agent？
- Codemap 与 language server / codegraph / grep 的边界在哪里？
