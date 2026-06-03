---
type: person
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
tags:
  - llm-wiki/entity/person
---
# Michael Bolin

## 在本 wiki 中的角色

Michael Bolin 是 OpenAI Codex 相关访谈的嘉宾；来源称其为 open source Codex tech lead。

## 来源支持的要点

- 他把 Codex harness 描述为 agent loop、tool execution 和 sandboxing/security policy 的组合。
- 他强调 Codex 倾向 small/tight harness、少量强工具，以及让 agent 自己探索代码库。
- 他区分 security 与 safety：前者偏本地权限和 sandbox，后者更多在模型侧判断 tool call 是否适合提出。
- 他认为 agent-first workflow 提升吞吐，但要求开发者学习管理多个并行 workstreams。

## 相关页面

- [[wiki/entities/products/Codex|Codex]]
- [[wiki/entities/products/Codex CLI|Codex CLI]]
- [[wiki/concepts/Sandbox and Tool Orchestration|Sandbox and Tool Orchestration]]
