---
type: source-summary
status: ingested
created: 2026-05-29
updated: 2026-05-29
source: "[[raw/2026-05-28 Harness design for long-running application development]]"
external_url: https://www.anthropic.com/engineering/harness-design-long-running-apps
author: Prithvi Rajasekaran
published: 2026-03-24
image_assets:
  - "[[raw/assets/2026-05-28-harness-design-solo-retro-game-maker.png]]"
  - "[[raw/assets/2026-05-28-harness-design-full-retro-game-maker.webp]]"
  - "[[raw/assets/2026-05-28-harness-design-dutch-museum.mp4]]"
  - "[[raw/assets/2026-05-28-harness-design-dutch-museum-frame-24s.jpg]]"
  - "[[raw/assets/2026-05-28-harness-design-browser-daw.mp4]]"
  - "[[raw/assets/2026-05-28-harness-design-browser-daw-frame.jpg]]"
tags:
  - llm-wiki/source
  - anthropic
  - harness-engineering
  - long-running-agents
  - multi-agent
---
# Harness design for long-running application development

## 一句话结论

Anthropic 把早期 initializer/coding-agent 长时程 harness 推进为 planner / generator / evaluator 三智能体架构：planner 扩展高层产品规格，generator 逐块构建，evaluator 用 Playwright 和明确评分标准做外部 QA；同时强调 harness 组件会随模型能力变化而失去或获得“承重性”。

## 来源元数据

- 原始资料： [[raw/2026-05-28 Harness design for long-running application development]]
- 外部链接： [Anthropic — Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
- 作者： [[wiki/entities/people/Prithvi Rajasekaran|Prithvi Rajasekaran]]
- 发表时间： 2026-03-24（官方页面显示；raw frontmatter 未记录）
- 本地媒体资产（ingest 时已读取）：
  - Solo 版 retro game maker： ![[raw/assets/2026-05-28-harness-design-solo-retro-game-maker.png]]
  - Full harness 版 retro game maker： ![[raw/assets/2026-05-28-harness-design-full-retro-game-maker.webp]]
  - 前端设计视频关键帧： ![[raw/assets/2026-05-28-harness-design-dutch-museum-frame-24s.jpg]]
  - Browser DAW 视频关键帧： ![[raw/assets/2026-05-28-harness-design-browser-daw-frame.jpg]]

## 关键要点

1. 文章延续 [[wiki/sources/2026-05-28 Effective harnesses for long-running agents|Effective harnesses for long-running agents]] 的两个核心经验：把任务分解为可处理 chunk，以及用结构化工件跨 session 传递上下文。
2. 早期方案仍有两个明显问题：长任务中模型会随 context 填满而失去连贯性或出现 “context anxiety”；agent 自评倾向过度乐观，尤其在设计这类主观质量任务中。
3. 作者借鉴 GAN 的 generator/evaluator 分离：让做事的 agent 与评价的 agent 分开，并通过明确、可校准的标准把主观判断变成可评分对象。
4. 在 frontend design 实验中，作者定义四类评分标准：design quality、originality、craft、functionality，并刻意提高 design quality 和 originality 的权重，以抵抗模板化/AI slop。
5. Evaluator 使用 [[wiki/entities/products/Playwright MCP|Playwright MCP]] 直接操作页面、截图并评分；5–15 轮迭代可推动 generator 走向更有辨识度的设计，但分数提升并不总是线性，复杂度也会增加。
6. Full-stack coding 版本采用 [[wiki/concepts/Planner-Generator-Evaluator Harness|Planner-Generator-Evaluator Harness]]：planner 把 1–4 句 prompt 扩展为完整产品规格；generator 按 sprint 或后续简化版按 build round 构建；evaluator 做用户视角 QA、API/数据库检查和多维评分。
7. Sprint 版本中，generator 与 evaluator 会先协商 [[wiki/concepts/Sprint Contract|Sprint Contract]]，明确每个 chunk 的 “done” 和可测试行为，再开始实现；通信通过文件完成。
8. Retro game maker 对比实验中，solo run 用 20 分钟/$9，full harness 用 6 小时/$200；full harness 成本高出 20x 以上，但 planner 产生 16-feature/10-sprint spec，最终 app 的可玩性、视觉一致性和功能深度明显更强。
9. QA agent 并非天然可靠。作者通过阅读 evaluator trace、找出与人类判断不一致的案例、更新 QA prompt，才让 evaluator 从“发现问题但说服自己放过”变成更严格的 reviewer。
10. Harness 简化原则：每个组件都编码了“当前模型做不到什么”的假设；随着 [[wiki/entities/products/Claude Opus 4.6|Claude Opus 4.6]] 等模型能力提升，应逐个移除或调整组件，识别哪些仍然 [[wiki/concepts/Load-bearing Harness Components|load-bearing]]。
11. Opus 4.6 版本移除了 sprint construct，保留 planner 和 evaluator，并把 evaluator 改成 end-of-run QA；结论是 evaluator 不是固定必需，而是在任务超出当前模型 solo 稳定能力边界时才值得成本。
12. DAW 实验中，更新版 harness 花费约 3 小时 50 分钟、$124.70；QA 仍抓到核心交互 display-only、录音 stub、clip 操作和效果可视化缺失等最后一公里问题。
13. 最终 DAW 并不专业，且 Claude 不能听音频导致音乐品味 QA 受限；但它具备浏览器内 arrangement view、mixer、transport 和可通过内置 agent 驱动的基本作曲流程。

## 需要更新的概念

- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Planner-Generator-Evaluator Harness|Planner-Generator-Evaluator Harness]]
- [[wiki/concepts/External Evaluator Agent|External Evaluator Agent]]
- [[wiki/concepts/Sprint Contract|Sprint Contract]]
- [[wiki/concepts/Load-bearing Harness Components|Load-bearing Harness Components]]
- [[wiki/concepts/Context Reset vs Compaction|Context Reset vs Compaction]]
- [[wiki/concepts/Self-verification|Self-verification]]
- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]]

## 需要更新的实体

- 人物： [[wiki/entities/people/Prithvi Rajasekaran|Prithvi Rajasekaran]], [[wiki/entities/people/Justin Young|Justin Young]]
- 组织： [[wiki/entities/organizations/Anthropic|Anthropic]]
- 产品/工具： [[wiki/entities/products/Claude Agent SDK|Claude Agent SDK]], [[wiki/entities/products/Claude Code|Claude Code]], [[wiki/entities/products/Playwright MCP|Playwright MCP]], [[wiki/entities/products/Claude Opus 4.5|Claude Opus 4.5]], [[wiki/entities/products/Claude Opus 4.6|Claude Opus 4.6]], [[wiki/entities/products/Claude Sonnet 4.5|Claude Sonnet 4.5]]

## 论断 / 证据

| 论断 | 证据 | 置信度 |
|---|---|---:|
| 将生成与评估分离，是改善主观和复杂 coding 任务的重要杠杆。 | 前端循环使用带校准标准的独立 evaluator；coding 循环使用 QA agent 抓到具体产品/API/数据库 bug。 | 中高：来源自述支持 |
| Planner agent 有助于防止短 prompt 导致范围过小。 | 移除 planner 后 generator 直接从原始 prompt 开始构建，应用功能更少；简化版 harness 仍保留 planner。 | 中高 |
| Evaluator 成本是否值得取决于任务和模型，不是普遍必需。 | 在 Opus 4.6 上，部分任务进入模型 solo 可靠边界内；evaluator 主要在接近或超过边界时仍有价值。 | 中高 |
| 随模型能力变化，harness 组件应定期压力测试。 | Opus 4.6 在长上下文、规划、代码审查和调试上提升后，作者逐个移除组件测试承重性。 | 高：设计原则 |
| 报告中的质量提升伴随显著成本和延迟。 | Retro game maker：solo 20 分钟/$9，full harness 6 小时/$200；DAW V2 harness 3 小时 50 分钟/$124.70。 | 高：来源报告数字；未独立验证 |

## 冲突 / 注意事项

- **Raw 元数据缺口：** raw frontmatter 中 `author` 与 `published` 为空；本页作者来自正文，发布日期来自官方页面。
- **来源自述：** 成本、质量和模型对比来自 Anthropic 自己的实验；本次 ingest 未复现。
- **Evaluator 限制：** QA 仍漏掉嵌套 bug、细微布局问题和不直观交互；Claude 不能听音频，也削弱了 DAW 示例中的音乐品味 QA。
- **成本/延迟：** 更强 harness 足够昂贵且慢，ROI 取决于任务价值、模型能力和可接受 wall-clock 时间。
- **Prompt 标准会塑造品味：** 标准文字提升了原创性，但也把设计推向特定视觉收敛，因此 evaluator 标准不是中性的。

## 后续问题

- 对特定模型/任务边界，如何判断 evaluator 是否值得成本？
- [[wiki/concepts/Sprint Contract|Sprint Contract]] 能否泛化到研究综合、金融建模等非代码工作？
- 该 planner/generator/evaluator 架构与 LangChain 的 tracing/self-verification 路线、Martin Fowler 的 feedforward/feedback 框架如何对比？
