---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering]]"
tags:
  - llm-wiki/concept
  - context-engineering
  - harness-engineering
---
# Local Context Injection

## 定义

本地上下文注入（Local Context Injection）是 harness 在 agent 开始工作前或工作中，主动收集并注入本地环境信息的机制，例如当前目录、目录结构、可用工具、运行约束、评分标准和编码规范。

## 为什么重要

Agent 自己探索未知环境容易浪费时间、漏掉关键工具或误判路径。由 harness 确定性地准备上下文，可以降低搜索错误面，让 agent 更快进入有效规划与验证。

## 来源支持的要点

- LangChain 用 `LocalContextMiddleware` 在 agent start 时映射 `cwd` 以及父/子目录。
- 该 middleware 还运行 bash 命令寻找 Python installations 等工具。
- 文章把这称为为 agent 做 context engineering 的 delivery mechanism。
- LangChain 还注入程序化评分约束、文件路径精确性、edge-case testing 和 time budget warnings。
- 该思路与 Böckeler 的 feedforward guides 相容：都是在生成前把环境和约束交给 agent。

## 相关概念

- [[wiki/concepts/Feedforward Guides|Feedforward Guides]]
- [[wiki/concepts/Agent-readable Codebase|Agent-readable Codebase]]
- [[wiki/concepts/Middleware Hooks|Middleware Hooks]]
- [[wiki/concepts/Harnessability|Harnessability]]

## 开放问题

- 注入多少上下文会从帮助变成噪音？
- 哪些上下文应每次自动扫描，哪些应缓存或版本化？
- 如何检测 agent 是否真正使用了注入的上下文？
