---
type: concept
status: draft
created: 2026-06-01
updated: 2026-06-01
aliases:
  - Tool budget
  - MCP context budget
sources:
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
tags:
  - llm-wiki/concept
  - context-management
  - mcp
  - plugins
---
# MCP and Plugin Context Budget

## 定义

MCP and Plugin Context Budget（MCP/插件上下文预算）是指在 Claude Code 或其他 coding agent 中控制已启用 MCP servers、plugins 和 tools 的数量与描述长度，避免它们占用过多上下文窗口、降低模型表现。

## 为什么重要

工具越多不等于能力越强。每个 MCP/plugin/tool 都可能带来工具说明、权限、状态和调用路径，挤占任务上下文并增加选择复杂度。好的 user harness 应允许“配置很多、按项目启用很少”。

## 来源支持的要点

- Claude Code shorthand 来源建议所有 MCP 可留在 user config，但未使用的全部 disable；通过 `/plugins` 或 `/mcp` 管理。
- 作者经验规则是：可以配置 20-30 个 MCP，但保持低于 10 个 enabled / 低于 80 tools active。
- 来源称过多工具会让 200k context window 在 compact 前实际只剩约 70k，并显著降低性能；该数字需视为个人经验。
- LangChain Anatomy 来源也把 skills/progressive disclosure 作为对抗 context rot 的 primitive，支持“能力按需披露”。

## 相关概念

- [[wiki/concepts/Context Rot|Context Rot]]
- [[wiki/concepts/Skills as Progressive Disclosure|Skills as Progressive Disclosure]]
- [[wiki/concepts/Context Engineering for Coding Agents|Context Engineering for Coding Agents]]
- [[wiki/entities/products/Model Context Protocol|Model Context Protocol]]

## 开放问题

- Tool count、tool description tokens、latency 和错误率之间如何量化？
- 项目级 disabled MCP 列表是否应进入 repo？
- 如何自动建议当前任务需要启用哪些 MCP，禁用哪些 MCP？
