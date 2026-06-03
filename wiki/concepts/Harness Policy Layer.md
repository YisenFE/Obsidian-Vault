---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
aliases:
  - Harness policy
  - Policy layer
sources:
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
tags:
  - llm-wiki/concept
  - harness-engineering
  - policy-layer
---
# Harness Policy Layer

## 定义

工作支架策略层（Harness Policy Layer）是 harness 中适合用自然语言表达的高层控制部分，包括角色、契约、证据要求、retry rules、validation strategy、state handoff 和 stopping conditions。它与 parser、tool execution、sandbox、logging、deterministic validators 等精确机制分离。

## 为什么重要

把 policy layer 显式化，可以避免 harness 逻辑完全埋进 controller code。这样团队能直接审查和比较 policy choices，也能在同一 runtime 下做 module ablation，判断某个 verifier、file-backed state 或 compression module 是否真正承重。

## 来源支持的要点

- 论文附录强调自然语言适合 harness policy，代码适合 exact mechanisms。
- RQ1 的简洁性审计显示，NLAH 能用更少静态材料表达可复用 policy。
- OSWorld 案例说明 policy layer 不必规定每个 action primitive；只要满足同一 completion contract，agent 可以选择不同具体路径。
- 论文把 explicit harness policy 视为把 harness 变成实验对象的前提。

## 相关概念

- [[wiki/concepts/Natural-Language Agent Harnesses|Natural-Language Agent Harnesses]]
- [[wiki/concepts/Artifact Contract|Artifact Contract]]
- [[wiki/concepts/Load-bearing Harness Components|Load-bearing Harness Components]]
- [[wiki/concepts/Harness Module Ablation|Harness Module Ablation]]

## 开放问题

- Policy layer 应以自由文本、YAML/Markdown schema，还是半结构 DSL 表达？
- 哪些 harness 规则必须下沉到 deterministic code，不能留在自然语言 policy 中？
- 如何对 policy layer 做版本管理、差异审查和安全扫描？
