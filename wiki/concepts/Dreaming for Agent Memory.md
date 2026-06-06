---
type: concept
status: draft
created: 2026-06-05
updated: 2026-06-05
aliases:
  - Dreaming
  - Dreams
  - Agent memory dreaming
  - Memory consolidation
sources:
  - "[[wiki/sources/2026-06-06 Agents that remember]]"
tags:
  - llm-wiki/concept
  - agent-memory
  - dreaming
  - managed-agents
  - multi-agent
---
# Dreaming for Agent Memory

## 定义

Dreaming for Agent Memory（智能体记忆整理）是对 agent 过去 session transcripts 和现有 memory store 的异步整理流程。它不是在 live session 中继续对话，而是在后台运行多智能体 harness，对记忆做事实核查、补充细节、合并重复、移除过时或矛盾内容，并生成新的 output memory store。

## 为什么重要

Memory store 解决了“session 之间不记得”的问题，但会引入第二个问题：agent 往往把每次任务都写进 memory，导致记忆无界增长、重复、陈旧和结构混乱。Dreaming 把长期记忆维护变成单独的 harness：执行 agent 负责工作时写入，dreaming harness 负责事后整理，使后续 session 更容易高效检索。

## 来源支持的要点

- Workshop 把 dreaming 定义为 asynchronous background job，输入是一个 memory store 和一组历史 sessions/transcripts。
- Dreaming harness 会做 fact-checking、enrich with details、dedupe、organize，并生成 output memory store。
- Dreaming 非破坏性：input memory store 不被直接修改，job 会写入新的 output memory store。
- Console 会展示 dream job 的状态、token usage 和 diff，便于 human-in-the-loop review。
- Dreaming 的内部结构是 multi-agent harness：orchestrator 负责派发 subagents，workshop 中说可按每个 input session 派一个 subagent，强调 exhaustive by design。
- 产物可以包含 index file 和带 metadata/slug 的具体 memory files，减少未来 agent 做宽泛 grep 的成本。
- Docs 补充：dreaming 是 research preview；输入支持 1 到 100 个 sessions；支持的模型包括 Claude Opus 4.8、Claude Opus 4.7 和 Claude Sonnet 4.6。

## 与其他机制的区别

- 与 [[wiki/concepts/Context Reset vs Compaction|Compaction]] 不同，dreaming 不只是压缩当前上下文，而是跨 session/transcript 维护一个长期 memory store。
- 与 [[wiki/concepts/Agent Memory Stores|Agent Memory Stores]] 不同，dreaming 关注 memory 的质量维护，而不是单次读写。
- 与 [[wiki/concepts/Dynamic Workflows|Dynamic Workflows]] 类似，dreaming 也使用多智能体 harness；但 dynamic workflows 是面向当前任务的现场 orchestration，dreaming 是异步、后台、记忆整理专用 orchestration。

## 相关概念

- [[wiki/concepts/Agent Memory Stores|Agent Memory Stores]]
- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]]
- [[wiki/concepts/File-backed State|File-backed State]]
- [[wiki/concepts/Dynamic Workflows|Dynamic Workflows]]
- [[wiki/concepts/Trace-driven Harness Iteration|Trace-driven Harness Iteration]]
- [[wiki/entities/products/Claude Managed Agents|Claude Managed Agents]]

## 开放问题

- Dreaming 的触发条件应该是定期、memory store 尺寸、staleness 信号，还是任务完成后？
- Dreaming 产出的 output store 如何 review 才足够严格但不阻塞 agent 迭代？
- Dreaming 发现的错误、偏好和流程模式应进入 memory store、rules file，还是正式 workflow/skill？
- 如何衡量 dreaming 对未来 session 的准确性、速度、成本和安全性的净收益？
