---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
aliases:
  - Tool output offloading
  - Tool call offloading
sources:
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
tags:
  - llm-wiki/concept
  - context-management
  - tools
---
# Tool Call Offloading

## 定义

工具调用卸载（Tool Call Offloading）是指当工具输出很大时，harness 不把完整输出塞入模型上下文，而是把完整结果写入文件系统，只把摘要、头尾片段、路径或检索入口返回给模型。

## 为什么重要

大型 stdout、日志、搜索结果或测试输出会快速污染上下文窗口。Offloading 保留可追溯原始证据，同时降低 context rot，让 agent 在需要时按需读取。

## 来源支持的要点

- LangChain Anatomy 文章描述：harness 可保留超过阈值工具输出的 head/tail tokens，并把完整输出 offload 到 filesystem。
- Bolin 访谈也说，对 gigabyte 级输出，应让 Codex 写入文件，再抓取需要部分，而不是直接放进上下文。
- 该机制依赖文件系统 primitive；否则被卸载的证据无法被后续 agent 稳定访问。

## 相关概念

- [[wiki/concepts/Context Rot|Context Rot]]
- [[wiki/concepts/Context Engineering for Coding Agents|Context Engineering for Coding Agents]]
- [[wiki/concepts/Filesystem as Harness Primitive|Filesystem as Harness Primitive]]
- [[wiki/concepts/File-backed State|File-backed State]]

## 开放问题

- head/tail 阈值、摘要方式和文件命名如何设计，才能既省上下文又不丢关键错误？
- Offloaded output 是否需要索引或 provenance 元数据？
- Agent 什么时候会主动回读完整输出，什么时候会被摘要误导？
