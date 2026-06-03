---
type: concept
status: draft
created: 2026-05-28
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 工程技术：在智能体优先的世界中利用 Codex]]"
tags:
  - llm-wiki/concept
  - codex
  - agent-first-development
---
# Codex-first Development

## 定义

Codex-first 开发（Codex-first Development）指以 [[wiki/entities/products/Codex|Codex]] 为主要代码生产者的软件开发方式：人类掌舵、定义目标和验收标准，智能体负责实现、测试、修复、审查反馈处理和部分合并流程。

## 为什么重要

这个概念把“AI 辅助编码”推进到“智能体优先的软件生产系统”。在该模式下，工程效率来自系统级杠杆：可读上下文、可执行工具、自动反馈、架构约束和持续清理，而不是人类单次写代码速度。

## 来源支持的要点

- OpenAI 文章声称，实验产品从空仓库开始，应用代码、测试、CI、文档、可观测性和内部工具都由 Codex 生成。
- 团队原则是“不手动编写代码”；人类主要把用户反馈转化为任务和验收标准，并验证结果。
- Codex 被要求本地审查自身变更、请求额外智能体审查、响应人类/智能体反馈，并循环直到审查满意。
- 文章报告了约一百万行代码、约 1,500 个 PR、三名工程师早期推动以及约 1/10 手工时间等指标；这些是来源自述，需独立验证。
- 最新阶段中，Codex 可以从提示开始复现 bug、录制故障视频、修复、验证、录制修复视频、开 PR、处理反馈、修构建、必要时升级给人类并合并。

## 相关概念

- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Agent-readable Codebase|Agent-readable Codebase]]
- [[wiki/concepts/Mechanized Invariants|Mechanized Invariants]]
- [[wiki/themes/智能体优先软件开发|Agent-first software development]]

## 开放问题

- “无人工代码”如何定义：是否包括脚本、配置、修复、复制粘贴、生成后编辑？
- 该内部产品的复杂度、质量和维护成本如何与传统团队对比？
- 对普通团队而言，Codex-first 是否需要先达到某个 harness 成熟度阈值？
