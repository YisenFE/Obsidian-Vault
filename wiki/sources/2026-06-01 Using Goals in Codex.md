---
type: source-summary
status: ingested
created: 2026-06-01
updated: 2026-06-01
source: "[[raw/2026-06-01 Using Goals in Codex]]"
external_url: https://developers.openai.com/cookbook/examples/codex/using_goals_in_codex
author: "[[wiki/entities/organizations/OpenAI|OpenAI]] / OpenAI Cookbook"
published: null
published_note: "Raw frontmatter has empty published and clipping-artifact author fields; raw unchanged."
image_assets:
  - "[[raw/assets/2026-06-01-codex-goals-01-goal-continuation-loop.png]]"
  - "[[raw/assets/2026-06-01-codex-goals-02-goal-thread-state.png]]"
  - "[[raw/assets/2026-06-01-codex-goals-03-goal-dispatcher-conditions.png]]"
  - "[[raw/assets/2026-06-01-codex-goals-04-strong-goal-components.png]]"
  - "[[raw/assets/2026-06-01-codex-goals-05-research-evidence-channels.png]]"
  - "[[raw/assets/2026-06-01-codex-goals-06-research-support-levels.png]]"
  - "[[raw/assets/2026-06-01-codex-goals-07-goal-final-output.png]]"
tags:
  - llm-wiki/source
  - openai
  - codex
  - goals
  - evidence-based-completion
---
# Using Goals in Codex

## 一句话结论

这篇 OpenAI Cookbook 文章把 Codex Goals 定义为线程级、持久的完成契约：用户不只是给下一步 prompt，而是声明一个可验证目标、约束、边界、迭代策略和阻塞停止条件；Codex 在安全的空闲边界继续工作，并且只有在具体证据支持时才能标记完成。

## 来源元数据

- 原始资料：[[raw/2026-06-01 Using Goals in Codex]]
- 外部链接：[OpenAI Cookbook — Using Goals in Codex](https://developers.openai.com/cookbook/examples/codex/using_goals_in_codex)
- 作者：[[wiki/entities/organizations/OpenAI|OpenAI]] / OpenAI Cookbook（raw frontmatter 的 author 字段像剪藏误抽取，未改 raw）
- 发表时间：待验证（raw frontmatter 为空）
- 本地图片资产（ingest 时已下载并查看）：
  - goal-continuation-loop: [[raw/assets/2026-06-01-codex-goals-01-goal-continuation-loop.png]]
  - goal-thread-state: [[raw/assets/2026-06-01-codex-goals-02-goal-thread-state.png]]
  - goal-dispatcher-conditions: [[raw/assets/2026-06-01-codex-goals-03-goal-dispatcher-conditions.png]]
  - strong-goal-components: [[raw/assets/2026-06-01-codex-goals-04-strong-goal-components.png]]
  - research-evidence-channels: [[raw/assets/2026-06-01-codex-goals-05-research-evidence-channels.png]]
  - research-support-levels: [[raw/assets/2026-06-01-codex-goals-06-research-support-levels.png]]
  - goal-final-output: [[raw/assets/2026-06-01-codex-goals-07-goal-final-output.png]]

## 关键要点

1. Goals 是 Codex 中的 persistent objectives（持久目标）：它们给 thread 附加一个完成条件，说明什么应为真、如何验证成功、哪些约束不能被破坏。
2. Goals 适合路径不确定但完成标准清晰的任务：性能调优、flaky test 复现、benchmark-driven tuning、bug hunt、多步 refactor、研究问题到证据审计。
3. Prompt 与 Goal 的差别是操作模型：prompt 是“做下一件事然后等”；Goal 是“围绕目标 work → check → continue or complete”。
4. Goal 不是无边界后台自治，而是 user-controlled completion contract；可以 pause、resume、clear、complete，也可能被 budget 或 blocker 停止。
5. Quickstart 命令包括 `/goal <outcome>`、`/goal` 查看、`/goal pause`、`/goal resume`、`/goal clear`；来源称 Goals 从 Codex 0.128.0 开始可用。
6. 一个强 Goal 通常包含六项：outcome、verification surface、constraints、boundaries、iteration policy、blocked stop condition。
7. 强 Goal 模板是：`/goal <desired end state> verified by <specific evidence> while preserving <constraints>. Use <allowed inputs, tools, or boundaries>. Between iterations, <policy>. If blocked, <report blocker and needed input>.`
8. Goal active 后有三类变化：目标持续可见；线程 idle 且 Goal active/in budget 时可继续；完成必须对照文件、测试、日志、benchmark、artifact 或研究证据。
9. 架构上，Goal 是 thread-scoped state（线程级状态），不是 global memory，也不是 project instructions；它记录 objective、lifecycle、budget、usage/progress accounting。
10. Continuation 是 event-driven 而非简单 while loop：Codex 只在 turn 完成、无 pending work、无 queued user input、thread idle 时检查继续。
11. Dispatcher 设计保守：plan-only work 不触发继续；interruptions 会 pause；如果 continuation turn 不做 tool call，会抑制下一次自动继续，避免空转。
12. Budget reached 不等于 complete；预算到达时应停止实质工作，报告进展、blockers 和下一步。
13. 工具权限边界也被限制：model 可以 start Goal，并且只在证据支持时 mark complete；pause/resume/clear/budget-limited transitions 由用户或系统控制。
14. 弱 Goal 如 `/goal Improve performance` 只给方向；强 Goal 如“把 checkout benchmark p95 降到 120ms 以下并保持 correctness suite green”给出目标、验证和约束。
15. 研究任务中，Goal 的价值是防止“生成看似完成的答案”：它要求 claim inventory、evidence mapping、feasible reproduction、blocked claims 和 remaining uncertainty 分层呈现。
16. Deep Hedging case study 中，Codex 能重建机制、近似训练、重建图表和数值检查，但因缺失原始 seeds、paths、checkpoints、optimizer state，只能给出 partial/approximate reproduction，而非 exact replay。
17. 不应使用 Goal 的场景：一行编辑、简单解释、短 code review、单次问答、完成线模糊的“make this better”、无法定义证据标准的任务。

## 术语说明

- Goal（目标）：Codex thread 上持久存在的完成契约，包含目标、状态、预算和证据检查。
- Completion contract（完成契约）：定义什么算完成、如何验证、哪些约束不能被破坏、何时应停止并报告阻塞。
- Verification surface（验证面）：测试、benchmark、日志、文件、artifact、报告或来源材料等可审计证据。
- Thread-scoped state（线程级状态）：Goal 属于当前 thread，而非全局记忆或项目说明。
- Continuation gate（继续门控）：Codex 是否能自动继续的安全边界，例如 thread idle、无 queued user input、Goal active、within budget。
- Budget-limited（预算受限）：预算耗尽后的状态；应报告进展和 blocker，不等于完成。
- Evidence-backed audit（证据支撑审计）：按 claim/evidence/status/uncertainty 分层输出，而不是把结果压成单一成功声明。

## 需要更新的概念

- [[wiki/concepts/Codex Goals|Codex Goals]]
- [[wiki/concepts/Goal Completion Contract|Goal Completion Contract]]
- [[wiki/concepts/Goal Lifecycle and Continuation Gates|Goal Lifecycle and Continuation Gates]]
- [[wiki/concepts/Evidence-Based Completion|Evidence-Based Completion]]
- [[wiki/concepts/Research Goal Audit|Research Goal Audit]]
- [[wiki/concepts/Artifact Contract|Artifact Contract]]
- [[wiki/concepts/Self-verification|Self-verification]]
- [[wiki/concepts/Agent Loop|Agent Loop]]
- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]]
- [[wiki/concepts/Context Engineering for Coding Agents|Context Engineering for Coding Agents]]

## 需要更新的实体

- 组织：[[wiki/entities/organizations/OpenAI|OpenAI]]
- 产品/工具：[[wiki/entities/products/Codex|Codex]]、[[wiki/entities/products/Codex CLI|Codex CLI]]

## 论断 / 证据

| 论断 | 证据 | 置信度 |
|---|---|---:|
| Goals 把 prompt 变成持久 outcome loop。 | 来源图示和正文对比 prompt: ask-work-result-wait 与 Goal: work-check-continue/complete。 | 高：来源直接定义 |
| 强 Goal 必须包含可审计完成标准。 | 来源列出 outcome、verification surface、constraints、boundaries、iteration policy、blocked stop condition。 | 高 |
| Goal 是 thread-scoped state，不是 global memory/project instruction。 | 架构段落明确说明 Goal 属于 current thread，记录 objective/status/budget/usage。 | 高 |
| Continuation 是保守事件驱动，不是无限循环。 | 来源列出 idle thread、无 queued input、无 pending work、no-tool-call suppression 等 gates。 | 高 |
| 完成必须由证据决定。 | 来源反复强调 tests/logs/benchmarks/artifacts/research evidence 决定完成，budget hit 不等于 complete。 | 高 |
| 研究 Goal 应输出 claim-level audit，而非夸大复现。 | Deep Hedging case study 将 reproduced mechanics、approximate trained results、blocked exact replay、uncertainty 分开。 | 高：来源案例支持 |

## 冲突 / 注意事项

- 该来源是 OpenAI Cookbook 指南，偏产品使用与设计说明，不是独立评测。
- Raw frontmatter 的 `author` 是剪藏误抽取，`published` 为空；本 wiki 未改 raw，只在来源摘要中标记待验证。
- Codex 0.128.0、命令表面、Goal lifecycle 和 UI 状态可能随产品版本变化。
- Goal continuation 不是无限后台 agent；它受 idle/thread/user input/budget/tool-call 等 gate 控制。
- “model can mark complete” 只在证据支持时成立；pause/resume/clear/budget-limited transitions 仍由用户或系统控制。

## 后续问题

- Goals 与 [[wiki/concepts/Artifact Contract|Artifact Contract]]、NLAH 的 stopping conditions 是否可以统一成一个“完成契约”模型？
- Goal budget 应如何设置：按 token、时间、turn、tool call，还是任务风险？
- 在团队代码库中，哪些任务应默认使用 Goal，而不是普通 prompt？
- Goal 的 progress accounting 如何与 git history、progress file、claim ledger 结合？
- 研究型 Goal 的证据等级是否可以标准化成 confirmed / approximate / support-only / blocked / uncertain？
