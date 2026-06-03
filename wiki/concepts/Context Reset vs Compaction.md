---
type: concept
status: draft
created: 2026-05-29
updated: 2026-06-03
sources:
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
  - "[[wiki/sources/2026-06-03 A harness for every task dynamic workflows in Claude Code]]"
tags:
  - llm-wiki/concept
  - context-management
  - long-running-agents
---
# Context Reset vs Compaction

## 定义

上下文重置（Context Reset）指清空当前上下文并启动新 agent，再通过结构化 handoff artifact 传递状态；上下文压缩（Compaction）指在同一个 agent 会话中压缩/总结早期历史，以便继续运行在较短上下文中。

## 为什么重要

长时程 agent 需要在上下文限制下保持任务连贯。Compaction 保留连续性但可能保留“context anxiety”；reset 给新 agent 一个 clean slate，但要求 handoff 足够完整，并增加 orchestration、token 和 latency 成本。

## 来源支持的要点

- Anthropic 早期 long-running harness 发现 compaction 不足以稳定支持跨多 context window 工作。
- 在 harness design 文章中，作者进一步指出 [[wiki/entities/products/Claude Sonnet 4.5|Claude Sonnet 4.5]] 的 context anxiety 明显，因此 context reset 对早期 harness 是关键解法。
- Reset 的代价是 handoff artifact 必须包含足够状态，否则新 agent 无法干净接手。
- [[wiki/entities/products/Claude Opus 4.5|Claude Opus 4.5]] 很大程度上移除了 context anxiety，因此新版 harness 可以不再使用 reset，而让 [[wiki/entities/products/Claude Agent SDK|Claude Agent SDK]] 的自动 compaction 处理 context growth。

- NLAH 论文的 module ablation 给出一个负面证据：context compression 在 SWE 和 OSWorld 上均降低 performance，作者总结为 durable state 比 aggressive compression 更可靠。
- 这并不推翻 compaction 的必要性，而是提示：压缩摘要如果与 evaluator 的成功标准漂移，就可能损失 task-critical 信息。
- Bolin 访谈把 context window、compaction 和大输出处理列为仍在积极追求的问题；他的经验是不要把 gigabyte 级工具输出直接塞进上下文，而是写入文件再按需读取。
- 这与 NLAH 的 file-backed state / compression ablation 互相补充：压缩不应替代可审计、可按需读取的持久状态。

- LangChain Anatomy 来源把 compaction 定义为当上下文窗口接近满时，harness 对既有上下文进行智能卸载和总结，使 agent 能继续工作。
- 同文把 tool call offloading 与 skills/progressive disclosure 作为 compaction 之外的 context-rot 防线，说明“压缩”只是上下文管理的一种策略。

- Claude Code dynamic workflows 来源把 goal drift 明确归因到长任务和 compaction 的有损摘要：边缘需求和 “不要做 X” 这类负约束可能丢失。
- Dynamic workflow 的另一种缓解方式不是继续压缩同一上下文，而是让多个子智能体拥有自己的干净上下文窗口和聚焦目标。

## 相关概念

- [[wiki/concepts/Context Engineering for Coding Agents|Context Engineering for Coding Agents]]

- [[wiki/concepts/File-backed State|File-backed State]]
- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]]
- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Load-bearing Harness Components|Load-bearing Harness Components]]
- [[wiki/themes/长时程智能体工作流|Long-running agent workflows]]

- [[wiki/concepts/Context Rot|Context Rot]]
- [[wiki/concepts/Tool Call Offloading|Tool Call Offloading]]
- [[wiki/concepts/Dynamic Workflows|Dynamic Workflows]]
- [[wiki/concepts/Long-running Agent Failure Modes|Long-running Agent Failure Modes]]

## 开放问题

- 如何检测当前模型是否出现 context anxiety？
- Handoff artifact 最小应包含哪些字段，才能安全使用 reset？
- 什么时候 reset 的 clean slate 价值超过它带来的成本和状态损失？
- 多子智能体 clean context 能否替代一部分 compaction，还是只把 handoff 问题转移到 workflow synthesis 阶段？
