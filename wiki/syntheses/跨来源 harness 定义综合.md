---
type: synthesis
status: draft
created: 2026-05-29
updated: 2026-05-29
aliases:
  - Harness definitions across sources
sources:
  - "[[wiki/sources/2026-05-28 工程技术：在智能体优先的世界中利用 Codex]]"
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
  - "[[wiki/sources/2026-05-28 Harness engineering for coding agent users]]"
  - "[[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering]]"
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
  - "[[wiki/sources/2026-06-01 Using Goals in Codex]]"
tags:
  - llm-wiki/synthesis
  - harness-engineering
  - definitions
---
# 跨来源 harness 定义综合

## 综合结论

这些来源共同认为：harness（智能体工作支架/运行环境）是模型外部让智能体工作更可靠的一整套环境、工具、约束、记忆、反馈和流程。但不同来源关注的边界不同：OpenAI 关注代码库和运行时环境，Anthropic 关注长任务交接和角色分工，Böckeler 关注用户能维护的外层 guides/sensors，LangChain 一条线索关注可实验调优的执行循环，另一条线索用 Agent = Model + Harness 给出 filesystem/bash/sandbox/context/verification 的 anatomy；NLAH 论文则把 harness policy 变成可执行、可审计、可消融的自然语言 representation object，Michael Bolin 的 Codex 访谈则补上了产品/运行时视角：agent loop、sandbox 与少量强工具如何支撑真实开发者机器上的 coding agent。

| 来源 | Harness 边界 | 主要控制问题 | 典型工件/工具 |
|---|---|---|---|
| OpenAI Codex-first engineering | 产品/团队代码库作为智能体运行环境 | 让 Codex 能行动、观察、验证，并保持在架构边界内 | 短 `AGENTS.md`、仓库文档、worktree、DevTools MCP、可观测性 API、自定义 lint、结构测试 |
| OpenAI Codex / Michael Bolin 访谈 | 产品/运行时 harness | 让模型在真实开发者机器上安全、可靠、高吞吐地行动 | Agent loop、terminal tool、sandbox policy、Codex App mission control、modest `AGENTS.md`、memory/context connectors |
| OpenAI Codex Goals | thread-scoped completion harness | 把一次性 prompt 变成围绕证据检查的持久目标循环 | `/goal` lifecycle、completion contract、verification surface、continuation gates、budget accounting、evidence-backed research audit |
| Anthropic effective long-running agents | 跨多个上下文窗口的 Agent SDK 工作流 | 保留进展，避免一次性做太多或过早完成 | Initializer prompt、coding agent prompt、feature list JSON、`claude-progress.txt`、git history、`init.sh`、浏览器测试 |
| Anthropic long-running app harness | 多智能体应用构建器 | 防止复杂/主观任务中范围过小和自评过弱 | Planner、generator、evaluator、Playwright MCP、sprint contract、评估标准、QA 日志 |
| Böckeler / MartinFowler.com | Coding agent 用户侧 outer harness | 让用户围绕自己的系统用生成前引导和反馈检测器调节 agent | AGENTS.md、skills、docs、LSP、CLI、codemod、review agent、静态分析、日志、浏览器、CI sensors |
| Claude Code shorthand / @affaan | 个人/用户侧 Claude Code operating harness | 把日常 agent 使用变成可复用、可观察、可限权、可并行的工作流 | Skills/commands、hooks、subagents、rules/memory、MCP/plugin budget、plugins、worktrees、tmux、editor integration、statusline |
| LangChain Agent Harness Anatomy | 通用 agent product harness | 把模型缺失的行为转化为 harness primitive | Filesystem + Git、bash/code execution、sandbox/default tooling、context rot management、Ralph Loop、planning、verification、model-harness training loop |
| LangChain Deep Agents | 可 benchmark 的 coding-agent 执行循环 | 在固定模型下通过 harness knob 提升分数、token 效率和延迟 | System prompt、tools、middleware、LangSmith traces、trace analyzer skill、build-verify loop、context injection、reasoning schedule |
| NLAH / IHR 论文 | 可执行自然语言 harness policy + shared runtime | 将 controller code 中隐藏的 policy 外化为可读、可迁移、可 ablate 的对象 | NLAH 文档、IHR、artifact contracts、file-backed state、module ablation、handoff metrics |

## 本 wiki 的工作定义

本 wiki 暂用以下定义：Harness Engineering（智能体工作支架工程）是设计模型运行环境、状态交接、工具、引导、检测器、约束、中间件、评估循环和角色结构的工程实践，目标是让智能体在更少人工监督下完成有用工作，并能更可靠地纠错；当 harness policy 被外化成 NLAH 这类文档时，它还可以成为可审计、可比较、可消融的研究对象。

这个定义需要区分五个相邻层次：

1. **模型与 agent 产品内置 harness**：系统提示词、检索、agent loop、sandbox、tool orchestration、上下文压缩、SDK/工具协议。
2. **项目/团队运行 harness**：仓库文档、架构规则、可观测性、CI、worktree、计划、功能契约。
3. **用户侧 outer harness**：团队围绕自己的 stack 和质量目标添加的 guides 与 sensors。
4. **harness 改进外循环**：trace、benchmark、错误分析 agent 和人类评审，用来调优 harness 本身。
5. **harness representation layer**：NLAH、skills、`AGENTS.md` 等可读 policy carriers，把 roles、contracts、evidence、handoff、validation 和 stopping conditions 显式化。

## 待讨论的张力

- 宽泛定义有解释力，但容易空泛；讨论具体控制时必须说明 bounded context。
- 更强 harness 往往消耗更多时间和 token；随着模型能力提升，不是每个组件都会继续承重。
- 行为正确性比维护性或架构边界更难 harness。
- 计算化控制与推断式控制的组合，取决于成本、确定性、任务风险和模型能力。
- 基于 trace 的优化能提高 benchmark 表现，但如果没有 held-out 任务或真实工作负载校验，可能过拟合。
- 自然语言适合表达 policy，但 parser、tool execution、sandbox、logging、validator 等 exact mechanism 仍应保留在代码层。
- Bolin/Codex 的 small-tool-surface 倾向强调少量强工具和强 sandbox；NLAH/IHR 倾向强调显式、可审计的 policy runtime，二者可能是互补层，也可能在“工具专用化程度”上存在张力。
- Model-harness co-evolution 说明，某些 harness primitive 会进入后训练并被模型吸收；但这也会让模型对特定 tool protocol 产生适配甚至过拟合，影响跨 harness 比较。
- Claude Code shorthand 进一步说明 user harness 也有“工具预算”问题：MCP/plugin 越多，能力越广，但上下文、延迟和选择复杂度也越高。
- Codex Goals 把 completion contract 产品化到 thread state 中；NLAH/IHR 把 completion/stopping policy 外化到自然语言 harness 中，二者都说明“完成”需要明确证据和停止条件。
- NLAH 论文显示 handoff 是 shared runtime 的主要弱点，说明“可执行自然语言 harness”仍需要强状态传递和权限边界。
