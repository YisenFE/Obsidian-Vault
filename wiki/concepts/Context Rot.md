---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
aliases:
  - Context rot
sources:
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
tags:
  - llm-wiki/concept
  - context-management
  - harness-engineering
---
# Context Rot

## 定义

上下文腐化（Context Rot）是指随着上下文窗口变长、变乱或塞入过多无关信息，模型的推理、定位和完成任务能力下降的现象。

## 为什么重要

长任务不是简单把更多 token 塞给模型。上下文里充满旧计划、巨大工具输出、过期假设和冗余说明时，agent 可能更慢、更贵，也更容易误判完成度。Harness 需要管理上下文的新鲜度、粒度和可检索性。

## 来源支持的要点

- LangChain Anatomy 文章引用 Context Rot，并认为现代 harness 很大程度是 good context engineering 的交付机制。
- 文章列出 compaction、tool call offloading、skills/progressive disclosure 三类应对策略。
- Bolin 访谈也强调大输出应写到文件，按需读取，而不是直接塞进 context window。
- NLAH 论文的 context compression ablation 提醒：压缩不一定总是正向，durable file-backed state 可能更可靠。

- Claude Code shorthand 来源给出工具层的 context rot 例子：启用太多 MCP/plugins/tools 会挤占上下文并降低性能。
- 作者经验是保留多个 MCP 在 user config 中，但按项目禁用不需要的 server；低于 10 个 enabled MCP / 80 active tools 是其经验规则。

## 相关概念

- [[wiki/concepts/Context Engineering for Coding Agents|Context Engineering for Coding Agents]]
- [[wiki/concepts/Context Reset vs Compaction|Context Reset vs Compaction]]
- [[wiki/concepts/Tool Call Offloading|Tool Call Offloading]]
- [[wiki/concepts/Skills as Progressive Disclosure|Skills as Progressive Disclosure]]
- [[wiki/concepts/File-backed State|File-backed State]]

- [[wiki/concepts/MCP and Plugin Context Budget|MCP and Plugin Context Budget]]

## 开放问题

- 如何用可观测指标检测 context rot？
- 什么时候该 compaction，什么时候该 reset，什么时候只应把状态写入文件？
- Skills/frontmatter 的最小加载粒度应如何设计？
