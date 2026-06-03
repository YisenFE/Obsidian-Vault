---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
tags:
  - llm-wiki/concept
  - tools
  - harness-engineering
---
# Small Powerful Tool Surface

## 定义

少量强工具界面（Small Powerful Tool Surface）是一种 agent harness 设计取向：减少专门工具数量，给 agent 少数通用且强大的操作原语，让模型自己选择如何组合工具完成任务。

## 为什么重要

更多专用工具可以把行为限制得更明确，但也可能让 harness 变重、让模型依赖作者预设路径。少量强工具保留模型探索空间，符合“让 agent 决定怎么做”的理念；但它更依赖 sandbox、权限控制和模型训练分布。

## 来源支持的要点

- Bolin 说 Codex 尽量把 harness 做得 small and tight，给少量 very powerful tools。
- Codex 不提供显式 read-file tool，而是给 terminal control，让模型用 `cat`、`sed` 等系统工具读文件。
- 当工具输出巨大时，Codex 可以把输出写入文件再按需读取，而不是把一大段内容塞入上下文窗口。
- Bolin 认为 terminal tool、memory、context connectors、browser/email/doc actions 等会继续成为未来工具原语的探索方向。

- LangChain Anatomy 来源从另一角度支持 small powerful tool surface：bash + code execution 让模型不用等待人类预先设计每个专用工具，而是临时写工具解决问题。
- 这种通用能力与 Codex terminal-first 思路一致，但更依赖 sandbox、network isolation 和默认工具配置来控制风险。

## 相关概念

- [[wiki/concepts/Sandbox and Tool Orchestration|Sandbox and Tool Orchestration]]
- [[wiki/concepts/Context Engineering for Coding Agents|Context Engineering for Coding Agents]]
- [[wiki/concepts/Load-bearing Harness Components|Load-bearing Harness Components]]
- [[wiki/concepts/Agent Loop|Agent Loop]]

- [[wiki/concepts/Bash and Code Execution|Bash and Code Execution]]

## 开放问题

- 哪些工具应该保持通用 terminal 形式，哪些必须做成专用工具？
- 少量强工具是否会增加安全审计难度？
- 如何判断一个 tool surface 是“足够小”而不是“过度贫瘠”？
