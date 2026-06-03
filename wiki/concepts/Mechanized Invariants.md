---
type: concept
status: draft
created: 2026-05-28
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 工程技术：在智能体优先的世界中利用 Codex]]"
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
  - "[[wiki/sources/2026-05-28 Harness engineering for coding agent users]]"
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
tags:
  - llm-wiki/concept
  - architecture
  - lint
---
# Mechanized Invariants

## 定义

机械化不变量（Mechanized Invariants）是把架构边界、可靠性要求、团队品味和任务验收边界转化为可自动检查、可阻断或可反馈的规则，例如自定义 lint、结构测试、类型约束、生成检查、不可随意改写的 feature list、codemods 和修复指令。

## 为什么重要

智能体会快速复制仓库中已有模式，包括坏模式。只靠文档无法长期维持完全由智能体生成的代码库的连贯性；把不变量编码到工具中，可以在高吞吐下持续约束输出，并把人类品味放大到每一次运行。

## 来源支持的要点

- OpenAI 文章主张强制执行不变量，而不是微观管理具体实现。
- 示例架构把每个业务域划成固定层：Types → Config → Repo → Service → Runtime → UI，并限制依赖方向和横切关注点入口。
- 自定义 lint 和结构测试用于强制边界、结构化日志、schema/type 命名、文件大小和平台可靠性要求。
- Lint 错误信息会写入智能体上下文中的修复指令，使失败本身成为可执行反馈。
- Anthropic 来源中的 JSON feature list 也是一种任务级不变量：agent 只能在验证后改 `passes`，不能删除或弱化测试描述。
- Böckeler 来源把结构测试、ArchUnit、dependency checks、mutation testing、coverage、static analysis 和 codemods 放进 computational controls；这些是最容易信任的 mechanized invariants。
- Böckeler 同时提醒：误解需求、错误诊断、过度设计和不必要功能并不能被这些机制可靠捕获。

- Claude Code shorthand 来源把部分团队偏好机械化为 hooks：编辑后自动格式化、运行 `tsc --noEmit`、扫描 `console.log`，push 前触发 review。
- 这说明自然语言规则可以逐步升级成确定性 hook/lint/test，以减少每次人工提醒。

## 相关概念

- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Agent-readable Codebase|Agent-readable Codebase]]
- [[wiki/concepts/Computational and Inferential Controls|Computational and Inferential Controls]]
- [[wiki/concepts/Feedback Sensors|Feedback Sensors]]
- [[wiki/concepts/Feature List as Test Contract|Feature List as Test Contract]]
- [[wiki/themes/智能体熵与垃圾回收|Agentic entropy and garbage collection]]

- [[wiki/concepts/Claude Code Hooks|Claude Code Hooks]]

## 开放问题

- 哪些规则应机械强制，哪些应保留给局部自主？
- 自定义 lint 的错误信息如何写，才能对智能体最有用？
- 如何从 inferential review 中提取可机械化的不变量？
- 哪些行为正确性要求仍然难以机械化？
