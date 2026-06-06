---
type: concept
status: draft
created: 2026-05-28
updated: 2026-06-05
sources:
  - "[[wiki/sources/2026-05-28 工程技术：在智能体优先的世界中利用 Codex]]"
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
  - "[[wiki/sources/2026-05-28 Harness engineering for coding agent users]]"
  - "[[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering]]"
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
  - "[[wiki/sources/2026-06-03 A harness for every task dynamic workflows in Claude Code]]"
  - "[[wiki/sources/2026-06-06 Agents that remember]]"
tags:
  - llm-wiki/concept
  - harness-engineering
---
# Harness Engineering

## 定义

智能体工作支架工程（Harness Engineering）是围绕智能体构建工作环境的工程实践：把目标、上下文、工具、反馈信号、验证机制、交接工件、角色分工、guides、sensors、middleware 和约束做成智能体能读取、执行、检查和持续改进的系统。

## 为什么重要

在 agent-first / long-running coding 中，瓶颈不再只是模型能不能写代码，而是智能体是否处在一个足够清晰、可观察、可验证、可恢复、可调节的环境中。不同来源给出的边界不同：OpenAI 强调仓库/运行时环境；Anthropic 强调 session handoff 与多 agent 角色；Böckeler 强调用户侧 guides/sensors；LangChain 强调 trace-driven experiment loop 和 middleware knobs。

## 来源支持的要点

- OpenAI 文章把工程师角色描述为设计环境、明确意图、构建反馈回路，而不是直接编写代码。
- OpenAI 把 UI、DOM、截图、导航、日志、指标、trace 接入智能体运行时，让 Codex 能复现、修复和验证行为。
- Anthropic long-running agent 来源用 initializer/coding-agent、`init.sh`、progress file、feature list 和 git history 处理跨 session 失忆、one-shotting 和过早完成。
- Anthropic application-development 来源引入 [[wiki/concepts/Planner-Generator-Evaluator Harness|Planner-Generator-Evaluator Harness]]，处理 under-scoping、自评偏乐观和浅层 QA。
- Böckeler 来源收窄到 coding-agent user harness：用户层 harness 是围绕特定系统放置的 [[wiki/concepts/Feedforward Guides|Feedforward Guides]] 与 [[wiki/concepts/Feedback Sensors|Feedback Sensors]]。
- Böckeler 把 harness 比作 cybernetic governor：通过 feedforward 和 feedback 把代码库调节到期望状态。
- LangChain 来源把 harness engineering 视为围绕固定模型优化 system prompt、tools、middleware、execution flow 等 knobs，以提升 performance、token efficiency 和 latency。
- LangChain 的关键方法是 [[wiki/concepts/Trace-driven Harness Iteration|Trace-driven Harness Iteration]]：用 traces 分析失败模式，再定向修改 harness。
- [[wiki/concepts/Load-bearing Harness Components|Load-bearing Harness Components]]、[[wiki/concepts/Harnessability|Harnessability]] 和 [[wiki/concepts/Reasoning Budgeting|Reasoning Budgeting]] 共同提示：harness 要和模型能力、代码库结构、任务风险、成本和反馈信号匹配。

- NLAH 论文补充了“harness 作为 representation object”的视角：[[wiki/concepts/Natural-Language Agent Harnesses|NLAH]] 把 run-level harness policy 写成可执行自然语言文档，[[wiki/concepts/Intelligent Harness Runtime|IHR]] 负责解释执行。
- NLAH 论文强调 policy/mechanism 分工：自然语言表达 roles、contracts、evidence、validation、state handoff 和 stopping conditions，代码仍承载 parsers、tool execution、sandbox、adapters、logging 与 deterministic validators。
- NLAH 的 RQ3 ablation 让 [[wiki/concepts/Load-bearing Harness Components|Load-bearing Harness Components]] 更可操作：file-backed state、self-evolution、evidence-backed answering 有正向证据；multi-candidate search 和 context compression 显示更多流程并不必然更好。

- Michael Bolin 访谈把 Codex harness 更具体地描述为 [[wiki/concepts/Agent Loop|agent loop]]、工具执行、sandbox policy 与少量强工具的组合。
- 该访谈补充了一种“small and tight harness”取向：尽量少写专门 wrapper，把更多决策空间留给模型；但用 [[wiki/concepts/Sandbox and Tool Orchestration|sandboxing]] 作为安全 backstop。
- Bolin 还把 harness reliability、performance 和资源节制列为关键原则：harness 崩溃会直接结束 session，因此它本身必须足够可靠。

- LangChain Anatomy 来源给出最宽定义：Agent = Model + Harness；harness 是把模型智能转成可行动工作系统的外部机制。
- 该来源用“想要的 agent 行为 → harness design”推导组件：filesystem/git、bash/code execution、sandbox/default tooling、memory/web/MCP、compaction/tool offloading/skills、Ralph Loop/planning/verification。
- 这篇文章还补充了 [[wiki/concepts/Model-Harness Co-evolution|Model-Harness Co-evolution]]：有用 primitive 会被加入 harness 并进入下一代模型训练循环，但也可能带来 tool-logic overfitting。

- Claude Code dynamic workflows 来源加入“动态生成 harness”的方向：Claude 可以按任务编写 JavaScript workflow，组合 classify-and-act、fan-out-and-synthesize、adversarial verification、tournament、loop until done 等模式。
- 该来源强调 harness engineering 需要做资源判断：workflow 更耗 token，适合复杂、高价值、对抗性或大规模并行任务，而不是所有 coding task 的默认流程。

- Agents that remember 来源把 harness engineering 推到长期记忆治理层：memory store 解决跨 session 读写，dreaming harness 解决长期 memory 的去重、过时、冲突和结构化问题。
- 该来源也强调权限和范围是 harness 设计问题：memory store 可以 read-only/read-write、per user/per workspace/per project，写权限错误可能污染未来 session。

## 相关概念

- [[wiki/concepts/Agent Loop|Agent Loop]]
- [[wiki/concepts/Sandbox and Tool Orchestration|Sandbox and Tool Orchestration]]
- [[wiki/concepts/Small Powerful Tool Surface|Small Powerful Tool Surface]]
- [[wiki/concepts/Context Engineering for Coding Agents|Context Engineering for Coding Agents]]

- [[wiki/concepts/Natural-Language Agent Harnesses|Natural-Language Agent Harnesses]]
- [[wiki/concepts/Intelligent Harness Runtime|Intelligent Harness Runtime]]
- [[wiki/concepts/Harness Policy Layer|Harness Policy Layer]]
- [[wiki/concepts/Harness Module Ablation|Harness Module Ablation]]
- [[wiki/concepts/Codex-first Development|Codex-first Development]]
- [[wiki/concepts/Coding Agent User Harness|Coding Agent User Harness]]
- [[wiki/concepts/Agent-readable Codebase|Agent-readable Codebase]]
- [[wiki/concepts/Repository as System of Record|Repository as System of Record]]
- [[wiki/concepts/Mechanized Invariants|Mechanized Invariants]]
- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]]
- [[wiki/concepts/Self-verification|Self-verification]]
- [[wiki/concepts/Middleware Hooks|Middleware Hooks]]
- [[wiki/concepts/Trace-driven Harness Iteration|Trace-driven Harness Iteration]]
- [[wiki/concepts/Computational and Inferential Controls|Computational and Inferential Controls]]
- [[wiki/concepts/Dynamic Workflows|Dynamic Workflows]]
- [[wiki/concepts/Long-running Agent Failure Modes|Long-running Agent Failure Modes]]
- [[wiki/concepts/Agent Memory Stores|Agent Memory Stores]]
- [[wiki/concepts/Dreaming for Agent Memory|Dreaming for Agent Memory]]

## 开放问题

- 如何把 harness policy 做成既可读、可执行、可审查，又不会引入 prompt injection 或危险工具链传播风险的对象？

- Codex 式 small/tight harness 与 NLAH/IHR 式可执行 policy runtime 如何取舍？

- Harness Engineering 的最小可行形态是什么：短 `AGENTS.md`、结构化 docs、session handoff、可观测性、自定义 lint、middleware，还是 external evaluator？
- 用户侧 harness 与平台/产品侧 harness 的边界在哪里？
- 如何评估 harness coverage、harness quality 和 harnessability？
- 如何避免 trace-driven optimization 过拟合某个 benchmark 或任务集？
- task-specific dynamic workflow 如何避免为了“更多流程”而制造额外成本和判断噪声？
- 长期 memory 的范围、权限、审计、清理和 review 应纳入 harness spec 的哪一层？
