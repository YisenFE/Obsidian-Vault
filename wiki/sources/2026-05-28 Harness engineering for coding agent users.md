---
type: source-summary
status: ingested
created: 2026-05-29
updated: 2026-05-29
source: "[[raw/2026-05-28 Harness engineering for coding agent users]]"
external_url: https://martinfowler.com/articles/harness-engineering.html
author: "[[wiki/entities/people/Birgitta Böckeler|Birgitta Böckeler]]"
published: 2026-04-02
image_assets:
  - "[[raw/assets/2026-05-28-fowler-harness-bounded-contexts.png]]"
  - "[[raw/assets/2026-05-28-fowler-harness-overview.png]]"
  - "[[raw/assets/2026-05-28-fowler-harness-change-lifecycle-examples.png]]"
  - "[[raw/assets/2026-05-28-fowler-harness-types.png]]"
  - "[[raw/assets/2026-05-28-fowler-harness-templates.png]]"
tags:
  - llm-wiki/source
  - harness-engineering
  - coding-agents
  - user-harness
  - thoughtworks
---
# Harness engineering for coding agent users

## 一句话结论

Birgitta Böckeler 把 coding agent 用户能控制的 “outer harness” 定义为一组 feedforward guides 与 feedback sensors：前者提高 agent 首次生成正确结果的概率，后者把问题尽量留在自修正循环中；核心工作是人类持续 steering 这些控制，而不是一次性写提示词。

## 来源元数据

- 原始资料： [[raw/2026-05-28 Harness engineering for coding agent users]]
- 外部链接： [MartinFowler.com — Harness engineering for coding agent users](https://martinfowler.com/articles/harness-engineering.html)
- 作者： [[wiki/entities/people/Birgitta Böckeler|Birgitta Böckeler]]
- 发表时间： 2026-04-02
- Earlier memo: 2026-02-17（本文说明该 memo 已被本文取代）
- 本地图片资产（ingest 时已读取）：
  - Bounded contexts 图： ![[raw/assets/2026-05-28-fowler-harness-bounded-contexts.png]]
  - Overview 图： ![[raw/assets/2026-05-28-fowler-harness-overview.png]]
  - Change lifecycle 图： ![[raw/assets/2026-05-28-fowler-harness-change-lifecycle-examples.png]]
  - Regulation categories 图： ![[raw/assets/2026-05-28-fowler-harness-types.png]]
  - Harness templates 图： ![[raw/assets/2026-05-28-fowler-harness-templates.png]]

## 关键要点

1. 文章从 LangChain 的 “Agent = Model + Harness” 宽定义出发，收窄到 coding agent 用户语境：模型外层还有 agent builder harness（系统提示词、检索、编排），最外层是用户为自己系统搭建的 user harness。
2. 一个好的 outer harness 有两个目标：提高 agent 一开始做对的概率，并在进入人类 review 前通过反馈循环自修正尽可能多的问题。
3. [[wiki/concepts/Feedforward Guides|Feedforward Guides]] 包括原则、CfRs、rules、reference docs、how-tos、language servers、CLI/scripts、codemods 等；它们进入初始生成阶段，约束或引导 agent。
4. [[wiki/concepts/Feedback Sensors|Feedback Sensors]] 包括 review agents、static analysis、logs、browser、linters、coverage、dependency/architecture checks、mutation testing 等；它们进入自修正、human review、pipeline 或连续监控阶段。
5. 文章区分 [[wiki/concepts/Computational and Inferential Controls|computational vs inferential controls]]：前者由 CPU 运行、确定性、快速可靠；后者依赖 LLM/语义判断，较慢、昂贵且非确定，但能覆盖语义/品味/高层判断。
6. 人类的核心工作是 **steering loop**：一旦某类问题反复出现，就改进 feedforward/feedback 控制，使它更少发生或被自动拦截；agent 也能帮助生成这些控制，例如结构测试、自定义 lint、规则草稿和 how-to guides。
7. 质量应尽量左移：便宜快速的 sensors 应在 commit 前或 agent 自修正循环中运行；昂贵、广域的 sensors 更适合在 integration/pipeline 或定期健康监测中运行。
8. 文章用 cybernetic governor 比喻 harness：通过 feedforward 和 feedback 将代码库调节到期望状态。
9. 文章把 coding-agent user harness 的调节维度分成三类：[[wiki/concepts/Harness Regulation Categories|maintainability harness]]、architecture fitness harness、[[wiki/concepts/Behaviour Harness|behaviour harness]]。其中 behaviour harness 最难，因为功能正确性仍大量依赖明确 spec、AI 生成测试、coverage/mutation testing 和人工验证。
10. [[wiki/concepts/Harnessability|Harnessability]] 指代码库能否被 harness 良好调节；强类型、清晰模块边界、成熟框架和可定义规则都会增加 harnessability。Legacy 系统往往最需要 harness，却最难构建 harness。
11. [[wiki/concepts/Harness Templates|Harness Templates]] 是把常见服务拓扑的结构、技术栈、guides 与 sensors 打包成模板；未来团队可能会按已有 harness 选择技术栈和结构，但会遇到模板版本化和同步问题。
12. 作者明确指出，maintainability/architecture 更容易 harness；behaviour harness、harness 覆盖率/质量评估、guides 与 sensors 的一致性仍是开放问题。

## 需要更新的概念

- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Coding Agent User Harness|Coding Agent User Harness]]
- [[wiki/concepts/Feedforward Guides|Feedforward Guides]]
- [[wiki/concepts/Feedback Sensors|Feedback Sensors]]
- [[wiki/concepts/Computational and Inferential Controls|Computational and Inferential Controls]]
- [[wiki/concepts/Harness Regulation Categories|Harness Regulation Categories]]
- [[wiki/concepts/Behaviour Harness|Behaviour Harness]]
- [[wiki/concepts/Harnessability|Harnessability]]
- [[wiki/concepts/Harness Templates|Harness Templates]]
- [[wiki/concepts/Mechanized Invariants|Mechanized Invariants]]

## 需要更新的实体

- 人物： [[wiki/entities/people/Birgitta Böckeler|Birgitta Böckeler]], [[wiki/entities/people/Martin Fowler|Martin Fowler]]
- 组织： [[wiki/entities/organizations/Thoughtworks|Thoughtworks]], [[wiki/entities/organizations/Stripe|Stripe]]
- 相关产品/工具： [[wiki/entities/products/Claude Code|Claude Code]], [[wiki/entities/products/ArchUnit|ArchUnit]], [[wiki/entities/products/OpenRewrite|OpenRewrite]], [[wiki/entities/products/Semgrep|Semgrep]]

## 论断 / 证据

| 论断 | 证据 | 置信度 |
|---|---|---:|
| Coding-agent 用户可以且应该在 agent 产品外构建 outer harness。 | 文章区分 model、builder harness 和 user harness，并聚焦用户能围绕自己系统放置的控制。 | 高：来源支持 |
| Feedforward + feedback 比“写更好的 prompt”更适合作为心智模型。 | 文章把 guides 定义为提高首次正确率，把 sensors 定义为在人类 review 前驱动自修正。 | 高 |
| 凡是可用的计算化控制，都应优先使用。 | 来源描述它们确定、快速、可靠，适合每次变更运行。 | 高 |
| 推断式控制有价值，但应按成本和非确定性放置。 | 文章认为 review agent / LLM judge 更慢、更贵且概率性更强，但适合语义判断。 | 高 |
| Behaviour harness 仍是最难的开放区域。 | 来源称 AI 生成测试加 coverage/人工测试，还不足以让监督显著减少。 | 高 |
| Harnessability 会影响技术栈和架构选择。 | 文章认为强类型、模块边界和框架会让更多控制可用；企业未来可能部分按 harness templates 选择技术栈。 | 中高：预测性论断 |

## 冲突 / 注意事项

- 文章是概念/经验框架，不是受控 benchmark。
- 文章明确提醒：计算化/推断式 sensors 不能可靠发现误解指令、不必要功能、过度工程化或错误问题诊断。
- 行为正确性仍然欠 harness 化；人类规格说明和人工测试仍很关键。
- Harness templates 会遇到与 service templates 类似的漂移/版本化问题，而且由于推断式 guides/sensors 更难测试，问题可能更重。
- Raw frontmatter 已包含 `author` 和 `published`；本次不需要修正 raw 元数据。

## 后续问题

- 类似 test coverage 或 mutation score 的“harness coverage”应该长什么样？
- 随着 harness 变大，团队如何保持 guides 与 sensors 一致？
- 这个用户侧 harness 模型如何映射到 OpenAI 的 Codex-first 仓库实践和 Anthropic 的多智能体 harness？
