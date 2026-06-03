---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
aliases:
  - Model-Harness Training Loop
  - Model harness co-evolution
sources:
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
  - "[[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering]]"
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
tags:
  - llm-wiki/concept
  - model-training
  - harness-engineering
---
# Model-Harness Co-evolution

## 定义

模型-支架共演化（Model-Harness Co-evolution）是指 agent 产品把有用 harness primitive 加入运行时后，下一代模型又在这些 primitive 和工具协议中后训练，因而更擅长使用该 harness；随后新的能力暴露新需求，循环继续。

## 为什么重要

这解释了为什么 harness 不是静态外壳：模型能力、工具协议、训练数据和产品体验会相互塑形。它也带来风险：模型可能对某个 tool logic 或 edit protocol 过拟合，换一种等价工具就表现下降。

## 来源支持的要点

- LangChain Anatomy 图示把循环描述为：发现 primitive → 加入 harness → 用 harness in the loop 训练下一代模型 → 模型更擅长使用 harness → 继续发现 primitive。
- 文章用 apply_patch tool logic 作为例子，说明改变工具逻辑可能让模型表现变差，显示后训练会绑定 harness 细节。
- 同文也强调最佳 harness 不一定是模型后训练时使用的 harness；Terminal Bench 例子显示只改 harness 仍可能显著改变表现。
- Bolin 访谈也提到 Codex 需要研究和工程共同开发，模型与 harness 都影响体验。

## 相关概念

- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Load-bearing Harness Components|Load-bearing Harness Components]]
- [[wiki/concepts/Small Powerful Tool Surface|Small Powerful Tool Surface]]
- [[wiki/concepts/Trace-driven Harness Iteration|Trace-driven Harness Iteration]]

## 开放问题

- benchmark 比较模型时，应如何控制 harness 差异？
- 哪些 harness primitive 会被模型能力吸收，哪些会长期留在系统层？
- 如何区分“模型真的更聪明”和“模型更适配某个 tool protocol”？
