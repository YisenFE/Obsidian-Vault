---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
tags:
  - llm-wiki/concept
  - agent-memory
  - state-management
---
# File-backed State

## 定义

文件承载状态（File-backed State）是把 agent run 的关键状态写入文件系统，让后续步骤、子 agent 或新 session 读取，而不是只依赖当前对话上下文或压缩摘要。

## 为什么重要

文件状态更持久、更可审计，也更容易作为 handoff artifact。NLAH 论文的 ablation 结果显示，file-backed state 在不同 benchmark 上都有正向作用；这与 Anthropic 用 progress file、feature list 和 git history 做长时程交接的经验相互印证。

## 来源支持的要点

- NLAH RQ3 中，file-backed state 在 SWE 上从 73.0 提升到 75.6，在 OSWorld 上从 44.4 提升到 58.3，是跨 benchmark 最强的正向模块之一。
- 论文附录还指出 durable state 比 aggressive compression 更可靠；context compression 在表 5 中对 SWE 与 OSWorld 都是负向。
- Anthropic 早期 long-running harness 使用 `claude-progress.txt`、feature list 和 git history 作为跨 session 状态层。

- LangChain Anatomy 来源将 filesystem 视为 file-backed state 的基础设施：agent 可以把中间输出、长期状态和协作痕迹写入 workspace，而不是全部留在上下文窗口。
- Git 进一步为 file-backed state 提供 history、rollback 和 branching，使新 agent 能通过文件与提交历史接续工作。

## 相关概念

- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]]
- [[wiki/concepts/Context Reset vs Compaction|Context Reset vs Compaction]]
- [[wiki/concepts/Repository as System of Record|Repository as System of Record]]
- [[wiki/concepts/Natural-Language Agent Harnesses|Natural-Language Agent Harnesses]]

- [[wiki/concepts/Filesystem as Harness Primitive|Filesystem as Harness Primitive]]
- [[wiki/concepts/Tool Call Offloading|Tool Call Offloading]]

## 开放问题

- 哪些状态必须 file-backed，哪些可以保留在上下文中？
- File-backed state 应按任务、session、agent role 还是 artifact type 分层？
- 如何自动检测 file-backed state 陈旧或相互冲突？
