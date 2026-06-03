---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
aliases:
  - IHR
sources:
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
tags:
  - llm-wiki/concept
  - harness-runtime
  - natural-language-harness
---
# Intelligent Harness Runtime

## 定义

智能工作支架运行时（Intelligent Harness Runtime，IHR）是执行 NLAH 文档的共享运行时：它把自然语言 harness policy 解释为 agent calls、handoffs、state updates、validation gates 和 artifact contracts，并把这些动作落到工具调用、文件状态和验证信号中。

## 为什么重要

如果 NLAH 只是普通 prompt，它只能软性提示模型；IHR 的价值在于提供 shared runtime semantics，让同一份 policy 可以跨任务运行、产生日志指标，并支持模块 ablation。它也是 NLAH 从“说明文字”变成“可执行对象”的关键。

## 来源支持的要点

- 论文用同一 IHR instantiation 跑 Live-SWE、MHTBA/TB2 和 OSWorld/SeeAct：Codex CLI 0.123.0、`gpt-5.4-mini`、reasoning effort `xhigh`。
- IHR-executed NLAHs 在三类 benchmark 中保持竞争性 task outcomes，但通常带来额外 model/tool calls 和 token 开销。
- RQ2 显示 IHR 能较好物化 artifact contract、tool call success 和 failed tool continuation。
- IHR 的主要弱点是 parent-child execution 中 handoff recall 较低，说明 runtime 需要更强的状态传递机制。
- 论文建议 deterministic hooks、sandbox、permission control、logging 和 validators 仍由代码层承担。

## 相关概念

- [[wiki/concepts/Natural-Language Agent Harnesses|Natural-Language Agent Harnesses]]
- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]]
- [[wiki/concepts/Middleware Hooks|Middleware Hooks]]
- [[wiki/concepts/File-backed State|File-backed State]]

## 开放问题

- IHR 应该提供哪些最小原语，才能执行大多数 NLAH 而不把 runtime 做成另一个复杂 controller？
- 如何在 IHR 中记录 handoff provenance，避免 parent-child execution 丢失关键信息？
- IHR 的权限、沙箱和 supply-chain 安全边界应如何设计？
