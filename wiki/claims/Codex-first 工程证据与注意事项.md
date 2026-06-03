---
type: claim-set
status: draft
created: 2026-05-28
updated: 2026-05-29
aliases:
  - Codex-first engineering evidence and caveats
sources:
  - "[[wiki/sources/2026-05-28 工程技术：在智能体优先的世界中利用 Codex]]"
tags:
  - llm-wiki/claim
  - codex
  - evidence
---
# Codex-first 工程证据与注意事项

## 范围

本页追踪 [[wiki/sources/2026-05-28 工程技术：在智能体优先的世界中利用 Codex|工程技术：在智能体优先的世界中利用 Codex]] 中的关键论断，并区分来源支持的说法与仍需独立验证的指标。

## 来源支持的论断

| 论断 | 来源证据 | 状态 |
|---|---|---|
| OpenAI 做过一个内部 Codex-first 产品实验，人类原则上不直接手写代码。 | 来源称团队有意禁止手工编码，并用 Codex 生成应用逻辑、测试、CI、文档、可观测性和内部工具。 | 来源支持；未独立验证 |
| 核心工程角色转向 harness 设计。 | 来源反复把人类工作描述为设计环境、意图、工具、抽象、约束和反馈回路。 | 来源支持 |
| 智能体可读的运行时信号能提升 QA 和自主性。 | 来源描述 worktree 应用实例、Chrome DevTools MCP、DOM 快照、截图、导航 skill 和本地可观测性查询 API。 | 来源支持 |
| 简短 `AGENTS.md` 应作为地图，而不是百科全书。 | 来源称巨型 instruction file 会占用上下文、指导效果差、容易腐化且难以机械检查。 | 来源支持 |
| 机械化架构约束是智能体高速工作的早期前提。 | 来源描述固定层级方向、受限依赖边、自定义 lint、结构测试和面向修复的错误信息。 | 来源支持 |
| 高吞吐智能体会改变合并经济学。 | 来源认为短 PR 生命周期和低成本后续修正，在该语境下可能优于长时间阻塞式 gate。 | 来源支持，但依赖具体上下文 |

## 待验证的量化论断

| 论断 | 为什么需要验证 | 验证状态 |
|---|---|---|
| 五个月后约一百万行代码。 | LOC 容易被生成文件放大，也不等同于产品复杂度。 | 待验证 |
| 打开并合并约 1,500 个 PR。 | PR 数可能反映小变更、自动重构或特定合并策略。 | 待验证 |
| 约为手工编码时间的 1/10。 | 没有基线时，反事实估算很难审计。 | 待验证 |
| 早期三名工程师、后期七名工程师提升吞吐。 | 对 staffing 判断有价值，但依赖隐藏的运营细节。 | 待验证 |
| 数百名内部 beta 用户和外部 alpha 测试者。 | 这关系到“真实产品”叙事是否成立。 | 待验证 |

## 注意事项

- 来源是 OpenAI 自己的工程博客，且内部产品未具名。
- 文章本身提醒：自主程度依赖特定代码库的工具和结构，不能直接外推。
- raw 中发布时间已修正为 2026-02-11。

## 相关页面

- [[wiki/concepts/Codex-first Development|Codex-first Development]]
- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/themes/智能体优先软件开发|智能体优先软件开发]]
