---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
  - "[[wiki/sources/2026-05-28 工程技术：在智能体优先的世界中利用 Codex]]"
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
  - "[[wiki/sources/2026-06-01 Using Goals in Codex]]"
tags:
  - llm-wiki/concept
  - context-engineering
  - coding-agents
---
# Context Engineering for Coding Agents

## 定义

编程智能体上下文工程（Context Engineering for Coding Agents）是在不过度规定解法的前提下，为 coding agent 提供任务目标、文件线索、仓库结构、测试方式、PR/GitHub 历史、文档和工具入口，并控制上下文体积与新鲜度的实践。

## 为什么重要

上下文太少会让 agent 像新员工一样误判；上下文太多又会挤占窗口、引入陈旧/重复信息，甚至让 agent 更差。好的 context engineering 是给 agent 足够线索和工具，让它能自己探索代码库，而不是把所有知识硬塞进 prompt。

## 来源支持的要点

- Bolin 自述给 Codex 的较大任务通常是一段 prompt，必要时提供文件指针；很多时候让 Codex 自己搜索代码库。
- 他强调文件和文件夹命名对 agent 搜索更重要，因为 Codex 会根据代码库模式和结构形成判断。
- GitHub/PR context 可以作为额外工具：例如类似问题发生在哪个 PR、哪个 PR 引入 regression。
- Codex 团队的 `AGENTS.md` 保持 modest，主要记录 agent 不容易从代码快速发现的信息，如测试如何运行、哪些测试更重要。
- 对大输出，Bolin 倾向让 Codex 写入文件再抓取需要部分，避免把 gigabyte 级输出直接放进上下文窗口。

- LangChain Anatomy 来源说，harnesses today are largely delivery mechanisms for good context engineering：核心工作是让 agent 在有限上下文里保留有用信息、卸载噪声、按需发现能力。
- Context rot 的应对策略包括 compaction、tool call offloading，以及 skills 的 progressive disclosure。
- 这补充了 Codex 访谈中的大输出写文件策略：上下文工程不只是“给更多材料”，也包括把材料移出上下文并提供可回读路径。

- Claude Code shorthand 来源把 context engineering 落到操作层：禁用未用 MCP/plugin、用 codemap 减少重复探索、用 statusline 观察 context 剩余比例、用 `/compact` 手动压缩。
- Editor integration、LSP plugins 和 `@` 文件搜索也属于上下文入口设计：它们帮助 agent/用户快速定位文件和类型信息。

- Codex Goals 来源把 context engineering 的一个目标写清楚：不只是给 Codex 更多材料，而是定义 evidence surface，让后续上下文围绕可审计目标收敛。
- 对研究任务，Goal 要求先定义 claim inventory、evidence route 和 uncertainty labels，防止上下文中的 plausible artifact 被误当成结论。

## 相关概念

- [[wiki/concepts/Agent-readable Codebase|Agent-readable Codebase]]
- [[wiki/concepts/Repository as System of Record|Repository as System of Record]]
- [[wiki/concepts/Feedforward Guides|Feedforward Guides]]
- [[wiki/concepts/Context Reset vs Compaction|Context Reset vs Compaction]]
- [[wiki/concepts/Small Powerful Tool Surface|Small Powerful Tool Surface]]

- [[wiki/concepts/Context Rot|Context Rot]]
- [[wiki/concepts/Tool Call Offloading|Tool Call Offloading]]
- [[wiki/concepts/Skills as Progressive Disclosure|Skills as Progressive Disclosure]]

## 开放问题

- `AGENTS.md` 的“modest”边界如何度量？
- 什么时候应给 agent 明确文件指针，什么时候应让它自行搜索？
- 如何自动发现 context 过量、陈旧或与代码冲突？
