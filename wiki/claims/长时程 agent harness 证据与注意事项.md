---
type: claim-set
status: draft
created: 2026-05-29
updated: 2026-05-29
aliases:
  - Long-running agent harness evidence and caveats
sources:
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
tags:
  - llm-wiki/claim
  - long-running-agents
  - harness-engineering
  - anthropic
---
# 长时程 agent harness 证据与注意事项

## 范围

本页追踪 [[wiki/sources/2026-05-28 Effective harnesses for long-running agents|Effective harnesses for long-running agents]] 中由来源支持的主要论断，并把可复用设计模式和仍需验证的边界分开。

## 来源支持的论断

| 论断 | 来源证据 | 状态 |
|---|---|---|
| 仅靠 context compaction 不足以支撑长时程 agent 工作。 | Anthropic 称即使有 compaction，跨多个上下文窗口仍会出现半成品无人记录和过早宣布胜利。 | 来源支持；未独立复现 |
| 第一次 session 应与后续 session 扮演不同角色。 | Initializer agent 在 coding agent 开始增量工作前创建 feature requirements、`init.sh`、`claude-progress.txt` 和初始 git 状态。 | 来源支持 |
| 功能需求应显式且结构化。 | 来源在 claude.ai clone 示例中使用包含 200 多个失败功能的 JSON feature list。 | 来源支持 |
| Agent 只能在端到端验证后标记功能通过。 | 文章称 Claude 否则容易在改完代码或跑窄测试后就标记完成；浏览器自动化改善了 Web 应用验证。 | 来源支持但为自述 |
| 干净交接需要 commit 和 progress notes。 | Coding agent 被提示写描述性 commit 和进展摘要，便于后续 session 恢复上下文。 | 来源支持 |

## 注意事项 / 局限

- 文章是 Anthropic 工程博客，报告的是内部实验；本 wiki 未复现 benchmark 或应用构建结果。
- 示例针对 full-stack web app 开发优化，跨领域泛化仍是来源自己提出的未来工作。
- 浏览器自动化不是完整 oracle：来源指出模型视觉/工具仍会漏掉浏览器原生 alert modal 等状态。
- “Separate agents” 在该文中指同一整体 harness 中的不同初始提示词，不一定是不同模型、系统提示词或工具配置。

## 后续待验证问题

| 问题 | 为什么重要 | 状态 |
|---|---|---|
| Initializer/coding-agent 分离带来多大提升？ | 文章给出定性改善，但 clipping 中没有受控量化指标。 | 待验证 |
| 在本 vault 工作流中，Markdown 任务列表是否比 JSON feature list 更容易退化？ | Anthropic 的 JSON 经验来自其场景；Obsidian-native 工作流可能不同。 | 待验证 |
| 专门 tester/QA agent 是否优于一个通用 coding agent？ | 文章把它列为未来工作。 | 待验证 |

## 相关页面

- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]]
- [[wiki/concepts/Feature List as Test Contract|Feature List as Test Contract]]
- [[wiki/concepts/Self-verification|Self-verification]]
- [[wiki/themes/长时程智能体工作流|长时程智能体工作流]]
