---
type: product
status: draft
created: 2026-06-05
updated: 2026-06-05
sources:
  - "[[wiki/sources/2026-06-06 Agents that remember]]"
tags:
  - llm-wiki/entity/product
  - anthropic
  - managed-agents
---
# Claude Managed Agents

## 在本 wiki 中的角色

Claude Managed Agents 是 Anthropic / Claude Platform 上的 managed agent 产品层，在本 wiki 中代表“平台托管的 agent harness”：它把 session、environment、memory stores、dreaming、multiagent orchestration、outcomes 等能力组合成可运行、可观察、可治理的 agent 环境。

## 来源支持的要点

- Agents that remember workshop 以 Claude Managed Agents 为背景，演示 session 默认隔离、memory store 挂载、Console/CLI 操作和 dreaming job。
- Memory store 作为 resource attached to session，使 agent 能跨 session 读写文件系统式记忆。
- Dreaming 作为异步 job 整理 memory store 和 session transcripts，产出 output memory store。
- 官方 docs 补充：memory stores 可通过 API/Console 管理、版本化和审计；dreaming 是 research preview。

## 相关概念

- [[wiki/concepts/Agent Memory Stores|Agent Memory Stores]]
- [[wiki/concepts/Dreaming for Agent Memory|Dreaming for Agent Memory]]
- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]]
- [[wiki/concepts/Harness Engineering|Harness Engineering]]

## 开放问题

- Claude Managed Agents 与 [[wiki/entities/products/Claude Agent SDK|Claude Agent SDK]]、[[wiki/entities/products/Claude Code|Claude Code]] 的产品边界如何长期演化。待验证。
