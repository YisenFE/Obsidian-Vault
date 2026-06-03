---
type: claim-set
status: draft
created: 2026-06-01
updated: 2026-06-01
aliases:
  - Codex Goals evidence and caveats
sources:
  - "[[wiki/sources/2026-06-01 Using Goals in Codex]]"
tags:
  - llm-wiki/claim
  - codex
  - goals
---
# Codex Goals 证据与注意事项

## 范围

本页追踪 OpenAI Cookbook “Using Goals in Codex” 关于 Goals 的用途、写法、生命周期、架构边界和研究任务用法的关键论断。

## 来源支持的论断

| 论断 | 来源证据 | 状态 |
|---|---|---|
| Goal 是 thread-scoped persistent objective。 | 来源说 Goal 是 persisted thread state，不是 global memory/project instruction。 | 来源支持 |
| Goal 适合路径不确定但完成标准清晰的任务。 | 来源列举 profiling、benchmarking、flaky test、research audit 等。 | 来源支持 |
| 强 Goal 应包含 outcome、verification surface、constraints、boundaries、iteration policy、blocked stop condition。 | “How to write a Goal” 段直接列出六项。 | 来源支持 |
| Completion 必须 evidence-based。 | 来源要求对照 files、tests、logs、benchmarks、artifacts、research evidence。 | 来源支持 |
| Continuation 是 event-driven 且保守。 | 来源列出 idle thread、无 queued input、plan-only 不继续、no-tool-call suppression 等。 | 来源支持 |
| Budget-limited 不等于 complete。 | 来源说预算到达时停止实质工作并报告 progress/blockers/next step。 | 来源支持 |
| Research Goal 能防止过度宣称。 | Deep Hedging 例子要求区分 approximate reproduction、blocked exact replay、uncertainty。 | 来源案例支持 |

## 注意事项 / 局限

- 来源是 OpenAI Cookbook 指南，反映产品设计和推荐用法，不是外部实验。
- Raw frontmatter 中 author/published 元数据不可靠：author 为剪藏误抽取，published 为空。
- Goals 命令表面、Codex 版本要求和生命周期行为可能随产品更新变化。
- 研究案例中的 Deep Hedging reproduction 是示例，不等于本文独立提供完整复现实验材料。
- 自动 continuation 仍受 thread idle、queued input、budget、tool call 等 gate 控制；不能理解为无限自治。

## 后续待验证问题

| 问题 | 为什么重要 | 状态 |
|---|---|---|
| Codex 0.128.0 之后 Goals 命令表面是否变化？ | 产品功能可能更新。 | 待验证 |
| Goal budget 的单位和默认策略是什么？ | 决定长任务成本和停止行为。 | 待验证 |
| Goal completion evidence 是否会被结构化记录？ | 影响审计和 handoff。 | 待验证 |
| Goals 与 AGENTS.md / project instructions / memory 的优先级关系是什么？ | 影响冲突处理。 | 待验证 |
| Research Goal audit 是否能成为通用研究复现模板？ | 影响本 wiki 后续论文复现/资料审计工作流。 | 待验证 |

## 相关页面

- [[wiki/concepts/Codex Goals|Codex Goals]]
- [[wiki/concepts/Goal Completion Contract|Goal Completion Contract]]
- [[wiki/concepts/Goal Lifecycle and Continuation Gates|Goal Lifecycle and Continuation Gates]]
- [[wiki/concepts/Evidence-Based Completion|Evidence-Based Completion]]
- [[wiki/concepts/Research Goal Audit|Research Goal Audit]]
