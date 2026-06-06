---
type: concept
status: draft
created: 2026-06-05
updated: 2026-06-05
aliases:
  - Memory Store
  - Claude Managed Agents memory store
  - Persistent agent memory store
sources:
  - "[[wiki/sources/2026-06-06 Agents that remember]]"
tags:
  - llm-wiki/concept
  - agent-memory
  - managed-agents
  - file-backed-state
---
# Agent Memory Stores

## 定义

Agent Memory Stores（智能体记忆存储）是供 agent 跨 session 读写的持久化文件系统式状态层。以 Claude Managed Agents 的 memory store 为例，它在创建 session 时作为 resource 挂载到 sandbox/container 中，agent 用普通文件工具读取、搜索、写入和组织记忆。

## 为什么重要

没有 memory store 时，session 之间默认相互隔离，agent 在前一次对话里学到的信息不会自动传给下一次。Memory store 把“跨 session 记忆”从 prompt stuffing 或手写 progress note 扩展成可版本化、可审计、可权限控制的文件系统资源，使 agent 能保存用户偏好、项目约定、历史错误、领域上下文和共享知识。

## 来源支持的要点

- workshop 演示了 base case：告诉第一个 session 新信息后，第二个 session 无法回忆。
- 创建并挂载 memory store 后，新 session 会先查 memory store，再回答上一 session 写入的信息。
- Memory store 可按 org、user、workspace、project 等边界创建，具体粒度由使用者定义。
- Memory store 可附带 instructions/prompt，告诉 agent 该 store 关注什么、应如何读写。
- 访问模式可分为 `read_write` 和 `read_only`；不需要写入的共享参考资料应避免开放写权限。
- 官方 docs 说明每个 memory 以 path 寻址、每次修改产生不可变 memory version，可用于审计和恢复。
- 官方 docs 还提示单个 session 最多挂载多个 stores，让不同生命周期、所有者和访问权限的 memory 分层。

## 设计含义

- Memory store 是 [[wiki/concepts/File-backed State|File-backed State]] 的产品化形态：记忆是文件，而不是隐式存在模型内部。
- Memory store 不是越大越好；过多、重复、过时或冲突的记忆会拖累检索和判断，需要 [[wiki/concepts/Dreaming for Agent Memory|Dreaming for Agent Memory]] 或人工 review 来整理。
- Memory store 的写权限是安全边界：读取不可信网页、聊天、工单或第三方内容的 agent 如果能写入共享 memory，可能把 prompt injection 或错误事实带入未来 session。

## 相关概念

- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]]
- [[wiki/concepts/File-backed State|File-backed State]]
- [[wiki/concepts/Filesystem as Harness Primitive|Filesystem as Harness Primitive]]
- [[wiki/concepts/Context Reset vs Compaction|Context Reset vs Compaction]]
- [[wiki/concepts/Dreaming for Agent Memory|Dreaming for Agent Memory]]
- [[wiki/entities/products/Claude Managed Agents|Claude Managed Agents]]

## 开放问题

- Memory store 的最佳边界是用户、团队、项目，还是任务类型？
- Shared store、personal store、project store 和 session-local store 的读写权限如何组合？
- 如何自动检测 memory 已经 stale、duplicated 或 contradicted？
- Memory store 与 repo 里的 `AGENTS.md` / `CLAUDE.md` / progress file 应如何分层？
