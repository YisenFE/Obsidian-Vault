---
type: concept
status: draft
created: 2026-05-28
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 工程技术：在智能体优先的世界中利用 Codex]]"
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
  - "[[wiki/sources/2026-05-28 Harness engineering for coding agent users]]"
tags:
  - llm-wiki/concept
  - documentation
  - context-management
---
# Repository as System of Record

## 定义

作为事实记录系统的仓库（Repository as System of Record）指把代码仓库作为智能体可访问的事实记录系统：架构、产品规范、执行计划、设计历史、质量评分、引用资料、技术债务、跨 session 进展、guides 和 sensors 配置都进入版本化结构，并由自动化保持新鲜。

## 为什么重要

智能体上下文有限，不能靠一次性塞入庞大说明书。仓库记录系统让智能体从短入口开始逐步发现相关上下文，同时让团队用 lint、CI 和定期维护任务检查文档是否过时、断链或缺失。用户侧 harness 也需要一个稳定位置来承载 architecture.md、AGENTS.md、skills、how-to guides、rules 和 sensor 配置。

## 来源支持的要点

- OpenAI 来源反对“一个巨大 AGENTS.md”模式，建议把 `AGENTS.md` 作为短入口/目录，指向更深的事实来源。
- 文档结构包括设计文档、执行计划、生成的 schema、产品规格、参考资料、架构/前端/质量/可靠性/安全等主题文件。
- 计划被视为一流工件：轻量计划、执行计划、决策日志、活跃/完成计划和技术债务 tracker 都进入版本控制。
- Anthropic 来源把 `claude-progress.txt` 与 git history 当作长时程 agent 的系统记录。
- Böckeler 来源中的 feedforward guides 包括 AGENTS.md、architecture.md、reference docs、how-tos、skills、API docs 和知识管理 MCP；这些都需要可维护的系统记录位置。
- Feedback sensors 的配置与结果也可能成为记录系统的一部分，例如 lint rules、structural tests、review-agent prompts 和 pipeline checks。

## 相关概念

- [[wiki/concepts/Agent-readable Codebase|Agent-readable Codebase]]
- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Feedforward Guides|Feedforward Guides]]
- [[wiki/concepts/Feedback Sensors|Feedback Sensors]]
- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]]

## 开放问题

- 对小团队而言，最小文档目录结构应该多厚？
- 文档 linter 应检查哪些信号：链接、owner、新鲜度、代码引用、还是测试覆盖？
- 外部文档系统如何与仓库记录系统保持一致？
- Guides 和 sensors 配置如何版本化并避免互相冲突？
