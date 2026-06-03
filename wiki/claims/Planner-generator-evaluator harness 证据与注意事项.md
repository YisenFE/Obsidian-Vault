---
type: claim-set
status: draft
created: 2026-05-29
updated: 2026-05-29
aliases:
  - Planner-generator-evaluator harness evidence and caveats
sources:
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
tags:
  - llm-wiki/claim
  - multi-agent
  - harness-engineering
  - anthropic
---
# Planner-generator-evaluator harness 证据与注意事项

## 范围

本页追踪 [[wiki/sources/2026-05-28 Harness design for long-running application development|Harness design for long-running application development]] 的主要论断，特别是多智能体 harness 的价值、成本、evaluator 可靠性，以及模型能力变化下的简化策略。

## 来源支持的论断

| 论断 | 来源证据 | 状态 |
|---|---|---|
| Generator/evaluator 分离能改善主观前端质量的迭代。 | 来源描述校准后的设计标准、基于 Playwright 的 evaluator 导航，以及 5–15 轮迭代让输出远离通用模板。 | 来源支持；自述 |
| Planner 能防止短 prompt 导致范围过小。 | 作者称移除 planner 后，generator 直接基于原始 prompt 构建，应用功能更少。 | 来源支持；自述 |
| 外部 evaluator 能抓到 generator 漏掉的 bug。 | Retro game maker evaluator 发现 UI/API/database bug；DAW evaluator 发现 display-only 或 stubbed 核心功能。 | 来源支持；有示例 |
| Evaluator 需要调优才足够严格。 | 早期 QA agent 会发现真实问题但随后批准；作者通过阅读日志调 prompt。 | 来源支持 |
| Harness 复杂度应随模型能力提升重新评估。 | Opus 4.6 提升后，作者移除 sprint structure，并把 evaluator 移到更靠后的阶段。 | 来源支持 |
| 更强 harness 可能显著更慢、更贵。 | Retro 对比：solo 20 分钟/$9，full harness 6 小时/$200；DAW 更新版 3 小时 50 分钟/$124.70。 | 来源报告数字；未独立验证 |

## 注意事项 / 局限

- 来源是 Anthropic 工程博客，结果更像说明性案例，而不是本 wiki 独立 benchmark。
- 对比不是等成本实验：full harness 花费了更多时间和 token。
- 人类判断仍然是 evaluator 校准的核心，尤其在主观品味和产品直觉上。
- QA 不完整：来源自己报告仍有嵌套 bug、交互不直观以及 Claude 不能听音频等 modality gap。
- 评分标准会塑造输出风格，evaluator prompt 既可能提升质量，也可能带来品味收敛。

## 后续待验证问题

| 问题 | 为什么重要 | 状态 |
|---|---|---|
| 如果 solo agent 获得相同 wall-clock/token 预算，质量提升还剩多少？ | 来源比较的是实践运行，不一定是严格预算对照。 | 待验证 |
| Evaluator 校准能否跨用户/团队标准化？ | 当前过程依赖作者偏好和 trace review。 | 待验证 |
| 哪些 harness 组件对非 Anthropic 模型或工具仍然承重？ | 简化逻辑可能可迁移，但具体组件未必相同。 | 待验证 |

## 相关页面

- [[wiki/concepts/Planner-Generator-Evaluator Harness|Planner-Generator-Evaluator Harness]]
- [[wiki/concepts/External Evaluator Agent|External Evaluator Agent]]
- [[wiki/concepts/Load-bearing Harness Components|Load-bearing Harness Components]]
- [[wiki/syntheses/Anthropic 长时程 harness 演化|Anthropic 长时程 harness 演化]]
