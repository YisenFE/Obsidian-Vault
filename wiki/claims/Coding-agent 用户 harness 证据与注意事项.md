---
type: claim-set
status: draft
created: 2026-05-29
updated: 2026-05-29
aliases:
  - Coding-agent user harness evidence and caveats
sources:
  - "[[wiki/sources/2026-05-28 Harness engineering for coding agent users]]"
tags:
  - llm-wiki/claim
  - harness-engineering
  - coding-agents
  - user-harness
---
# Coding-agent 用户 harness 证据与注意事项

## 范围

本页追踪 [[wiki/sources/2026-05-28 Harness engineering for coding agent users|Harness engineering for coding agent users]] 中关于用户侧 outer harness、生成前引导、反馈检测器、计算化/推断式控制，以及 behaviour harness 开放问题的关键论断。

## 来源支持的论断

| 论断 | 来源证据 | 状态 |
|---|---|---|
| “Harness” 必须说明 bounded context。 | 来源区分模型、builder harness 和 coding agent 用户围绕自己系统搭建的 user harness。 | 来源支持的框架 |
| 用户侧 harness 应结合 feedforward guides 与 feedback sensors。 | 来源图示和正文把控制分为引导初始生成的 guides，以及驱动自修正的 sensors。 | 来源支持的框架 |
| 能计算化的控制应优先计算化。 | 来源描述 computational controls 确定、快速、可靠，可在每次变更中运行。 | 来源支持 |
| 推断式控制能补充语义判断，但必须按成本放置。 | 来源认为 AI review / LLM-as-judge 更慢、更贵且非确定，但适合语义判断。 | 来源支持 |
| 可维护性和架构比行为正确性更容易 harness。 | 来源指出维护性/架构已有成熟工具，而 behaviour 是“elephant in the room”。 | 来源支持 |
| Harness templates 可能成为企业平台资产。 | 来源预测常见服务模板会演化为带拓扑特定 harness 的模板。 | 预测性论断；来源支持 |

## 注意事项 / 局限

- 文章是心智模型和实践经验综合，不是带量化效果的实验。
- 计算化/推断式 sensors 仍无法可靠发现误解需求、不必要功能、错误诊断或过度工程化。
- 行为正确性仍较弱；没有强规格和人类判断时，AI 生成测试不足以替代验收。
- Harness templates 会继承服务模板的漂移问题，并加入更难测试的非确定性控制。
- “Harnessability” 在来源中是定性概念，尚未定义度量方式。

## 后续待验证问题

| 问题 | 为什么重要 | 状态 |
|---|---|---|
| 如何度量 harness 覆盖率？ | Böckeler 明确提出需要类似代码覆盖率或 mutation testing 的 harness 质量指标。 | 待验证 |
| 哪些重复 review 反馈最适合转化成计算化控制？ | 这是从推断式判断走向确定性检查的实际路径。 | 待验证 |
| 用户侧 harness 在真实团队中能减少多少 review toil？ | 来源认为这是目标，但没有量化。 | 待验证 |

## 相关页面

- [[wiki/concepts/Coding Agent User Harness|Coding Agent User Harness]]
- [[wiki/concepts/Feedforward Guides|Feedforward Guides]]
- [[wiki/concepts/Feedback Sensors|Feedback Sensors]]
- [[wiki/concepts/Behaviour Harness|Behaviour Harness]]
- [[wiki/syntheses/跨来源 harness 定义综合|跨来源 harness 定义综合]]
