---
type: index
status: active
created: 2026-05-28
updated: 2026-06-05
tags:
  - llm-wiki/index
---
# Wiki 索引

本页是 `wiki/` 的内容目录。回答问题或 ingest 新来源前，先读这里。

## 核心入口

- [[wiki/overview|总览]] — 当前知识库的高层综合与研究边界。
- [[wiki/log|日志]] — 追加式操作日志。
- [[AGENTS|LLM Wiki 维护规范]] — 维护本 wiki 的规则和工作流。
- [[Karpathy wiki 方法论]] — 方法论来源说明。

## 来源资料

> 状态说明：`raw-only` 表示已有原始资料但尚未生成 `wiki/sources/` 摘要页；`ingested` 表示已生成来源摘要并更新相关 wiki 页。

| 来源 | 状态 | 备注 |
|---|---:|---|
| [[wiki/sources/2026-05-28 工程技术：在智能体优先的世界中利用 Codex|工程技术：在智能体优先的世界中利用 Codex]] | ingested | OpenAI：Codex-first 软件产品实验；人类掌舵、智能体执行；仓库记录系统、可观测性反馈回路、机械不变量与 AI 垃圾回收。 |
| [[wiki/sources/2026-05-28 Effective harnesses for long-running agents|Effective harnesses for long-running agents]] | ingested | Anthropic：长时程 agent；initializer/coding agent；feature list、progress file、git history、`init.sh` 与端到端浏览器验证。 |
| [[wiki/sources/2026-05-28 Harness design for long-running application development|Harness design for long-running application development]] | ingested | Anthropic：planner/generator/evaluator；外部 evaluator、sprint contract、Playwright QA、模型能力变化下的 harness 简化。 |
| [[wiki/sources/2026-05-28 Harness engineering for coding agent users|Harness engineering for coding agent users]] | ingested | Birgitta Böckeler：coding-agent 用户侧 outer harness；feedforward guides、feedback sensors、computational/inferential controls、harnessability。 |
| [[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering|Improving Deep Agents with harness engineering]] | ingested | LangChain：Terminal Bench；trace-driven harness iteration、build-verify loop、middleware、context injection、reasoning budgeting。 |
| [[wiki/sources/2026-05-28 Natural-Language Agent Harnesses|Natural-Language Agent Harnesses]] | ingested | arXiv：NLAH 与 IHR；把 harness policy 外化为可执行自然语言对象，并用 benchmark、机制指标和 module ablation 评估。 |
| [[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents|OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]] | ingested | Turing Post / Michael Bolin：Codex agent loop、sandbox/security、small tool surface、Codex App 与 agent-first developer workflow。 |
| [[wiki/sources/2026-05-28 The Anatomy of an Agent Harness|The Anatomy of an Agent Harness]] | ingested | LangChain：Agent = Model + Harness；filesystem/git、bash/code execution、sandbox/default tooling、context rot、Ralph Loop 与 model-harness co-evolution。 |
| [[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code|The Shorthand Guide to Everything Claude Code]] | ingested | @affaan：Claude Code 日常 operating harness；skills/commands、hooks、subagents、rules/memory、MCP/plugin context budget、worktrees/tmux、editor integration。 |
| [[wiki/sources/2026-06-01 Using Goals in Codex|Using Goals in Codex]] | ingested | OpenAI Cookbook：Codex Goals；thread-scoped completion contract、verification surface、continuation gates、budget accounting、research audit。 |
| [[wiki/sources/2026-06-03 A harness for every task dynamic workflows in Claude Code|A harness for every task: dynamic workflows in Claude Code]] | ingested | Claude blog：Claude Code dynamic workflows；按任务生成 JavaScript 多智能体 harness，组合 fan-out、对抗验证、tournament、loop until done、模型路由和 worktree 隔离。 |
| [[wiki/sources/2026-06-06 Agents that remember|Agents that remember]] | ingested | Claude workshop：Claude Managed Agents memory stores 与 dreaming；用文件系统式记忆跨 session 持久化，并用异步多智能体 harness 整理长期记忆。 |

## 概念

> 下面的英文名词按领域常用写法保留；每个不直观术语都要在对应概念页用中文解释。

- [[wiki/concepts/Agent Harness 术语表|Agent Harness 术语表]] — 保留英文核心术语时使用的中文解释表。
- [[wiki/concepts/Harness Engineering|Harness Engineering]] — 智能体工作支架工程：设计工具、上下文、反馈信号、交接工件、角色分工、guides/sensors、middleware 和约束，使智能体可靠工作。
- [[wiki/concepts/Agent Harness|Agent Harness]] — 智能体工作支架：模型之外让智能体可行动、可记忆、可验证的系统层。
- [[wiki/concepts/Filesystem as Harness Primitive|Filesystem as Harness Primitive]] — 文件系统/git 作为 agent 的持久状态层、协作面和上下文卸载面。
- [[wiki/concepts/Bash and Code Execution|Bash and Code Execution]] — 用 bash/代码执行给 agent 通用工具能力。
- [[wiki/concepts/Context Rot|Context Rot]] — 上下文变长/变脏导致模型表现下降的现象。
- [[wiki/concepts/Tool Call Offloading|Tool Call Offloading]] — 大型工具输出写文件，只把摘要或路径放进上下文。
- [[wiki/concepts/Skills as Progressive Disclosure|Skills as Progressive Disclosure]] — 技能按需加载，减少启动上下文噪声。
- [[wiki/concepts/Ralph Loop|Ralph Loop]] — 拦截退出并用 clean context 继续长任务的 harness pattern。
- [[wiki/concepts/Model-Harness Co-evolution|Model-Harness Co-evolution]] — 模型与 harness primitive 在产品和训练循环中相互塑形。
- [[wiki/concepts/Claude Code Operating Harness|Claude Code Operating Harness]] — Claude Code 个人操作支架：skills、hooks、subagents、rules、MCP/plugins、worktrees、tmux、editor、statusline。
- [[wiki/concepts/Dynamic Workflows|Dynamic Workflows]] — Claude Code 动态工作流：由 Claude 按任务生成 JavaScript 多智能体 workflow，动态组合模型、worktree、验证和停止条件。
- [[wiki/concepts/Long-running Agent Failure Modes|Long-running Agent Failure Modes]] — 长时程智能体失败模式：agentic laziness、自我偏好偏差、goal drift 及其 harness 防线。
- [[wiki/concepts/Claude Code Hooks|Claude Code Hooks]] — Claude Code 工具调用/生命周期事件上的自动化反馈和 guardrails。
- [[wiki/concepts/Subagent Scoping|Subagent Scoping]] — 用有限角色、工具、MCP 和权限约束子智能体。
- [[wiki/concepts/MCP and Plugin Context Budget|MCP and Plugin Context Budget]] — 管理启用 MCP/plugins/tools 对上下文窗口和性能的消耗。
- [[wiki/concepts/Parallel Agent Workflows|Parallel Agent Workflows]] — 用 `/fork`、git worktrees、tmux 等组织并行 agent 工作流。
- [[wiki/concepts/Agent Rules and Memory|Agent Rules and Memory]] — 用 CLAUDE.md / rules folder 表达长期规则、偏好和记忆。
- [[wiki/concepts/Codemaps for Agents|Codemaps for Agents]] — checkpoint 更新代码地图，帮助 agent 快速导航代码库。
- [[wiki/concepts/Codex Goals|Codex Goals]] — Codex 线程级持久目标，把 prompt 转成证据检查的持续工作循环。
- [[wiki/concepts/Goal Completion Contract|Goal Completion Contract]] — 目标完成契约：outcome、verification surface、constraints、boundaries、iteration policy、blocked stop condition。
- [[wiki/concepts/Goal Lifecycle and Continuation Gates|Goal Lifecycle and Continuation Gates]] — Goal 状态、pause/resume/clear、budget 和自动继续门控。
- [[wiki/concepts/Evidence-Based Completion|Evidence-Based Completion]] — 只有测试、日志、benchmark、artifact 或研究证据支持时才声明完成。
- [[wiki/concepts/Research Goal Audit|Research Goal Audit]] — 面向研究/复现任务的 claim/evidence/status/uncertainty 审计模式。
- [[wiki/concepts/Natural-Language Agent Harnesses|Natural-Language Agent Harnesses]] — 自然语言智能体工作支架：用自然语言文档描述 run-level harness policy。
- [[wiki/concepts/Agent Loop|Agent Loop]] — 智能体循环：模型提出 tool call，harness 执行并返回结果。
- [[wiki/concepts/Sandbox and Tool Orchestration|Sandbox and Tool Orchestration]] — 沙箱与工具编排：让 agent 工具调用在权限边界内运行。
- [[wiki/concepts/Safety vs Security in Agentic Systems|Safety vs Security in Agentic Systems]] — 区分模型侧安全行为与本地权限/隔离边界。
- [[wiki/concepts/Small Powerful Tool Surface|Small Powerful Tool Surface]] — 少量强工具：用更少、更通用的工具给 agent 更大探索空间。
- [[wiki/concepts/Context Engineering for Coding Agents|Context Engineering for Coding Agents]] — 编程智能体上下文工程：给足线索与工具，避免过量/陈旧上下文。
- [[wiki/concepts/Intelligent Harness Runtime|Intelligent Harness Runtime]] — 智能工作支架运行时：解释 NLAH 并执行 agent calls、handoffs、state updates、validation gates 和 artifact contracts。
- [[wiki/concepts/Harness Policy Layer|Harness Policy Layer]] — 工作支架策略层：适合自然语言表达的角色、契约、证据、验证、交接和停止条件。
- [[wiki/concepts/Artifact Contract|Artifact Contract]] — 产物契约：把完成条件绑定到可审计文件、证据或验收工件。
- [[wiki/concepts/File-backed State|File-backed State]] — 文件承载状态：把关键状态写入文件系统，供后续步骤、子 agent 或新 session 读取。
- [[wiki/concepts/Harness Module Ablation|Harness Module Ablation]] — 工作支架模块消融：评估各 harness module 是否真正承重。
- [[wiki/concepts/Coding Agent User Harness|Coding Agent User Harness]] — coding agent 用户为特定系统搭建的外层工作支架。
- [[wiki/concepts/Codex-first Development|Codex-first Development]] — 人类掌舵、Codex 执行的软件开发模式。
- [[wiki/concepts/Agent-readable Codebase|Agent-readable Codebase]] — 对智能体可发现、可查询、可验证、可恢复的代码库与运行环境。
- [[wiki/concepts/Repository as System of Record|Repository as System of Record]] — 把 docs、计划、架构、质量、技术债务、guides/sensors 和跨 session 进展放进版本化仓库。
- [[wiki/concepts/Mechanized Invariants|Mechanized Invariants]] — 用 lint、结构测试、feature contract、codemod 等机制强制架构、品味和验收不变量。
- [[wiki/concepts/Feedforward Guides|Feedforward Guides]] — 生成前引导：在生成前引导 agent 的原则、rules、docs、skills、LSP、CLI、codemods 等。
- [[wiki/concepts/Feedback Sensors|Feedback Sensors]] — 生成后反馈检测器：在生成后检测问题并反馈给 agent、人类、pipeline 或 harness 改进外循环。
- [[wiki/concepts/Computational and Inferential Controls|Computational and Inferential Controls]] — 确定性计算控制与 LLM/语义推断控制的取舍。
- [[wiki/concepts/Harness Regulation Categories|Harness Regulation Categories]] — maintainability、architecture fitness、behaviour 等 harness 调节维度。
- [[wiki/concepts/Behaviour Harness|Behaviour Harness]] — 调节功能行为是否符合需求的最难 harness 类别。
- [[wiki/concepts/Harnessability|Harnessability]] — 代码库/架构/技术栈被 harness 有效调节的难易程度。
- [[wiki/concepts/Harness Templates|Harness Templates]] — 面向常见服务拓扑预打包的 guides/sensors 模板。
- [[wiki/concepts/Trace-driven Harness Iteration|Trace-driven Harness Iteration]] — 用 LangSmith/trace 等失败证据迭代改进 harness。
- [[wiki/concepts/Build-Verify Loop|Build-Verify Loop]] — 规划/构建/验证/修复的 agent 自验证循环。
- [[wiki/concepts/Middleware Hooks|Middleware Hooks]] — 围绕模型/工具调用的可编程 agent-loop 拦截点。
- [[wiki/concepts/Local Context Injection|Local Context Injection]] — harness 主动注入目录、工具、约束和评估标准。
- [[wiki/concepts/Reasoning Budgeting|Reasoning Budgeting]] — 在计划、构建、验证阶段分配不同推理预算。
- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]] — 用 progress file、git history、feature list 等外化状态桥接 context/session。
- [[wiki/concepts/Agent Memory Stores|Agent Memory Stores]] — 智能体记忆存储：挂载到 session 的持久文件系统式状态层，用于跨 session 保存和读取记忆。
- [[wiki/concepts/Dreaming for Agent Memory|Dreaming for Agent Memory]] — 智能体记忆整理：异步读取 memory store 与历史 transcripts，生成去重、更新、结构化后的 output memory store。
- [[wiki/concepts/Feature List as Test Contract|Feature List as Test Contract]] — 把功能清单作为不可随意改写的验收契约。
- [[wiki/concepts/Self-verification|Self-verification]] — 让 agent 在声明完成前运行端到端、用户视角、可复现验证。
- [[wiki/concepts/Planner-Generator-Evaluator Harness|Planner-Generator-Evaluator Harness]] — planner 定规格、generator 构建、evaluator 外部 QA 的多智能体 harness。
- [[wiki/concepts/External Evaluator Agent|External Evaluator Agent]] — 独立于执行 agent 的怀疑式评价/QA agent。
- [[wiki/concepts/Sprint Contract|Sprint Contract]] — generator/evaluator 在实现前协商的 “done” 和可测试行为契约。
- [[wiki/concepts/Load-bearing Harness Components|Load-bearing Harness Components]] — 随模型和任务变化而承重或失效的 harness 组件。
- [[wiki/concepts/Context Reset vs Compaction|Context Reset vs Compaction]] — clean slate reset 与上下文压缩的长任务取舍。

## 实体

### 人物

- [[wiki/entities/people/Ryan Lopopolo|Ryan Lopopolo]] — OpenAI Codex-first engineering 文章作者。
- [[wiki/entities/people/Justin Young|Justin Young]] — Anthropic long-running agents 文章作者。
- [[wiki/entities/people/Prithvi Rajasekaran|Prithvi Rajasekaran]] — Anthropic Labs 成员；planner/generator/evaluator harness 文章作者。
- [[wiki/entities/people/Birgitta Böckeler|Birgitta Böckeler]] — coding-agent 用户侧 harness engineering 文章作者。
- [[wiki/entities/people/Vivek Trivedy|Vivek Trivedy]] — LangChain Deep Agents harness engineering 文章作者。
- [[wiki/entities/people/Michael Bolin|Michael Bolin]] — OpenAI Codex open-source tech lead；Codex harness 访谈嘉宾。
- [[wiki/entities/people/affaan|@affaan]] — Claude Code shorthand 来源作者。
- [[wiki/entities/people/Thariq Shihipar|Thariq Shihipar]] / [[wiki/entities/people/Sid Bidasaria|Sid Bidasaria]] — Claude Code dynamic workflows 文章作者。
- [[wiki/entities/people/Ksenia|Ksenia]] — Turing Post / Inference 访谈者。
- [[wiki/entities/people/Linyue Pan|Linyue Pan]] / [[wiki/entities/people/Lexiao Zou|Lexiao Zou]] / [[wiki/entities/people/Shuo Guo|Shuo Guo]] / [[wiki/entities/people/Jingchen Ni|Jingchen Ni]] / [[wiki/entities/people/Hai-Tao Zheng|Hai-Tao Zheng]] — NLAH 论文作者。
- [[wiki/entities/people/Martin Fowler|Martin Fowler]] — MartinFowler.com 主理人/网站关联人物。
- [[wiki/entities/people/Victor Zhu|Victor Zhu]] — 文章致谢贡献者。
- [[wiki/entities/people/Zach Brock|Zach Brock]] — 文章致谢贡献者。

### 组织 / 产品

- [[wiki/entities/organizations/OpenAI|OpenAI]] / [[wiki/entities/products/Codex|Codex]] / [[wiki/entities/products/Codex CLI|Codex CLI]] / [[wiki/entities/products/Codex App|Codex App]] / [[wiki/entities/products/GPT-5|GPT-5]] / [[wiki/entities/products/GPT-5.2-Codex|GPT-5.2-Codex]] / [[wiki/entities/products/GPT-5.4-Mini|GPT-5.4-Mini]]
- [[wiki/entities/organizations/Anthropic|Anthropic]] / [[wiki/entities/products/Claude Agent SDK|Claude Agent SDK]] / [[wiki/entities/products/Claude Code|Claude Code]] / [[wiki/entities/products/Claude Managed Agents|Claude Managed Agents]] / [[wiki/entities/products/Claude Platform|Claude Platform]]
- [[wiki/entities/organizations/LangChain|LangChain]] / [[wiki/entities/products/Deep Agents|Deep Agents]] / [[wiki/entities/products/LangSmith|LangSmith]]
- [[wiki/entities/organizations/Tsinghua University Shenzhen International Graduate School|Tsinghua University Shenzhen International Graduate School]] / [[wiki/entities/organizations/Harbin Institute of Technology (Shenzhen)|Harbin Institute of Technology (Shenzhen)]]
- [[wiki/entities/organizations/Turing Post|Turing Post]]
- [[wiki/entities/products/SWE-bench Verified|SWE-bench Verified]] / [[wiki/entities/products/Live-SWE-Agent|Live-SWE-Agent]]
- [[wiki/entities/products/Terminal Bench|Terminal Bench]] / [[wiki/entities/products/MHTBA|MHTBA]] / [[wiki/entities/products/Meta-Harness|Meta-Harness]]
- [[wiki/entities/products/OSWorld|OSWorld]] / [[wiki/entities/products/SeeAct|SeeAct]]
- [[wiki/entities/products/LinguaClaw|LinguaClaw]]
- [[wiki/entities/products/VS Code|VS Code]] / [[wiki/entities/products/JetBrains|JetBrains]] / [[wiki/entities/products/Xcode|Xcode]]
- [[wiki/entities/products/Model Context Protocol|Model Context Protocol]] / [[wiki/entities/products/Zed|Zed]] / [[wiki/entities/products/Cursor|Cursor]] / [[wiki/entities/products/tmux|tmux]] / [[wiki/entities/products/mgrep|mgrep]] / [[wiki/entities/products/hookify|hookify]] / [[wiki/entities/products/Supabase|Supabase]] / [[wiki/entities/products/GitHub Actions|GitHub Actions]]
- [[wiki/entities/products/Harbor|Harbor]] / [[wiki/entities/products/Daytona|Daytona]]
- [[wiki/entities/organizations/Thoughtworks|Thoughtworks]] / [[wiki/entities/organizations/Stripe|Stripe]]
- [[wiki/entities/products/Claude Opus 4.5|Claude Opus 4.5]] / [[wiki/entities/products/Claude Opus 4.6|Claude Opus 4.6]] / [[wiki/entities/products/Claude Opus 4.7|Claude Opus 4.7]] / [[wiki/entities/products/Claude Sonnet 4.5|Claude Sonnet 4.5]] / [[wiki/entities/products/Claude Sonnet 4.6|Claude Sonnet 4.6]]
- [[wiki/entities/products/Claude Opus 4.8|Claude Opus 4.8]] / [[wiki/entities/products/Bun|Bun]]
- [[wiki/entities/products/Aardvark|Aardvark]]
- [[wiki/entities/products/Chrome DevTools MCP|Chrome DevTools MCP]]
- [[wiki/entities/products/Puppeteer MCP|Puppeteer MCP]] / [[wiki/entities/products/Playwright MCP|Playwright MCP]]
- [[wiki/entities/products/ArchUnit|ArchUnit]] / [[wiki/entities/products/OpenRewrite|OpenRewrite]] / [[wiki/entities/products/Semgrep|Semgrep]]
- LangGraph（待建）

## 主题 / 综合 / 论断

- [[wiki/themes/智能体优先软件开发|智能体优先软件开发]] — 智能体优先开发的初始综合。
- [[wiki/themes/长时程智能体工作流|长时程智能体工作流]] — 跨 context/session 的长时程 agent 工作流模式。
- [[wiki/themes/智能体熵与垃圾回收|智能体熵与垃圾回收]] — AI 生成代码的漂移与持续清理。
- [[wiki/syntheses/跨来源 harness 定义综合|跨来源 harness 定义综合]] — 当前已 ingest 来源对 harness 边界的定义对照。
- [[wiki/syntheses/Anthropic 长时程 harness 演化|Anthropic 长时程 harness 演化]] — Anthropic 长时程 harness 从 session continuity、planner/generator/evaluator 到 dynamic workflows 的演化综合。
- [[wiki/claims/Codex-first 工程证据与注意事项|Codex-first 工程证据与注意事项]] — OpenAI 来源中的关键论断、量化指标与待验证项。
- [[wiki/claims/长时程 agent harness 证据与注意事项|长时程 agent harness 证据与注意事项]] — Anthropic initializer/coding-agent harness 的关键论断与边界。
- [[wiki/claims/Planner-generator-evaluator harness 证据与注意事项|Planner-generator-evaluator harness 证据与注意事项]] — Anthropic planner/generator/evaluator harness 的关键论断、成本与边界。
- [[wiki/claims/Coding-agent 用户 harness 证据与注意事项|Coding-agent 用户 harness 证据与注意事项]] — 用户侧 outer harness 的关键论断与未解问题。
- [[wiki/claims/Deep Agents harness engineering 证据与注意事项|Deep Agents harness engineering 证据与注意事项]] — LangChain Deep Agents / Terminal Bench harness 改进论断与边界。
- [[wiki/claims/NLAH 证据与注意事项|NLAH 证据与注意事项]] — NLAH/IHR 的可行性、机制指标、module ablation 与安全边界。
- [[wiki/claims/Codex harness 访谈证据与注意事项|Codex harness 访谈证据与注意事项]] — Michael Bolin 访谈中的 Codex harness、sandbox、tool surface 与 workflow 论断。
- [[wiki/claims/Agent harness anatomy 证据与注意事项|Agent harness anatomy 证据与注意事项]] — LangChain Anatomy 中 Agent = Model + Harness、filesystem/bash/sandbox/context rot、Ralph Loop 与 model-harness co-evolution 论断。
- [[wiki/claims/Claude Code shorthand 证据与注意事项|Claude Code shorthand 证据与注意事项]] — @affaan Claude Code 配置实践中的 user harness、MCP/tool budget、hooks、subagents 和并行工作流论断。
- [[wiki/claims/Codex Goals 证据与注意事项|Codex Goals 证据与注意事项]] — OpenAI Cookbook 中 Goals 的用途、写法、生命周期、继续门控、预算和研究审计论断。
- [[wiki/claims/Claude Code dynamic workflows 证据与注意事项|Claude Code dynamic workflows 证据与注意事项]] — Claude Code dynamic workflows 的多智能体 JavaScript harness、模式、成本边界和待验证项。
- [[wiki/claims/Claude Managed Agents memory 与 dreaming 证据与注意事项|Claude Managed Agents memory 与 dreaming 证据与注意事项]] — Claude Managed Agents memory stores、dreaming、权限边界、非破坏性 output store 与待验证项。
- 待创建：Codex、Claude Agent SDK、LangChain、NLAH/IHR 在 harness 设计上的差异。

## 问题

- [[wiki/questions/Claude Code 有必要使用 memory store 和 dreaming 吗|Claude Code 有必要使用 memory store 和 dreaming 吗]] — 判断 Claude Code 日常使用是否需要引入 Claude Managed Agents 的 memory store / dreaming，以及更合适的分层。
