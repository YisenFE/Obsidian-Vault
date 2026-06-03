---
type: claim-set
status: draft
created: 2026-05-29
updated: 2026-05-29
aliases:
  - Anatomy of an Agent Harness evidence and caveats
sources:
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
tags:
  - llm-wiki/claim
  - agent-harness
  - langchain
---
# Agent harness anatomy 证据与注意事项

## 范围

本页追踪 LangChain “The Anatomy of an Agent Harness” 对 agent harness 组成、核心 primitive、长时程执行、context rot 与模型-支架共演化的主要论断，并标注来源边界。

## 来源支持的论断

| 论断 | 来源证据 | 状态 |
|---|---|---|
| Agent = Model + Harness。 | 文章 TLDR 与结尾直接写明模型包含智能、harness 让智能有用。 | 来源定义 |
| 模型天然不具备 durable state、code execution、realtime knowledge、environment setup。 | “Why Do We Need Harnesses” 段逐项列出。 | 来源支持 |
| Filesystem + Git 是基础 harness primitive。 | 文章称 filesystem arguably the most foundational primitive，并解释 storage、context offload、collaboration；git 提供 rollback/branch/history。 | 来源支持的设计判断 |
| Bash + code execution 是通用工具策略。 | 文章把 bash 描述为避免为每个动作预设工具，让模型 on the fly 写工具。 | 来源支持的设计判断 |
| Sandboxes 同时解决安全、规模和默认工具配置。 | 文章描述隔离执行、allow-list、network isolation、on-demand environments、preinstalled tooling。 | 来源支持 |
| Context rot 需要 compaction、tool offloading、skills/progressive disclosure。 | “Battling Context Rot” 段明确列出这些策略。 | 来源支持 |
| 长时程执行依赖 filesystem/git、Ralph Loop、planning、self-verification。 | “Long Horizon Autonomous Execution” 段按这些子机制展开。 | 来源支持 |
| 模型与 harness 共演化，但可能出现 tool-logic overfitting。 | “The Coupling of Model Training and Harness Design” 段讨论后训练与 apply_patch 例子。 | 来源支持的判断，需验证 |

## 注意事项 / 局限

- 文章主要是概念框架，不是新的 benchmark 实验；Terminal Bench 相关内容引用 LangChain 其他文章和排行榜。
- “filesystem 最基础”“bash/code exec 优于预设工具”等是强工程取向，需和 NLAH/IHR 的显式 policy runtime、专用工具协议做对照。
- Ralph Loop 能对抗 early stopping，但如果完成定义不清，可能导致循环延长、过度修改或目标漂移。
- Model-harness co-evolution 解释了工具协议适配，但没有量化不同工具变体的性能退化幅度。
- 来源发布时间点的产品/模型名与 benchmark 状态可能变化；本页只记录来源时点陈述。

## 后续待验证问题

| 问题 | 为什么重要 | 状态 |
|---|---|---|
| filesystem/bash/sandbox 是否构成最小 agent harness？ | 影响本 wiki 对 harness 层次的 canonical 定义。 | 待验证 |
| Tool call offloading 的摘要策略会不会遗漏关键错误？ | 关系到上下文节省与证据完整性的平衡。 | 待验证 |
| Ralph Loop 与 artifact contract / external evaluator 如何组合？ | 关系到 long-running agent 的停止条件和质量门。 | 待验证 |
| 模型对 apply_patch 等工具逻辑的 overfitting 有多强？ | 关系到模型评估和工具协议迁移。 | 待验证 |

## 相关页面

- [[wiki/concepts/Agent Harness|Agent Harness]]
- [[wiki/concepts/Filesystem as Harness Primitive|Filesystem as Harness Primitive]]
- [[wiki/concepts/Bash and Code Execution|Bash and Code Execution]]
- [[wiki/concepts/Context Rot|Context Rot]]
- [[wiki/concepts/Ralph Loop|Ralph Loop]]
- [[wiki/concepts/Model-Harness Co-evolution|Model-Harness Co-evolution]]
