---
type: glossary
status: active
created: 2026-05-29
updated: 2026-06-05
sources:
  - "[[wiki/index]]"
  - "[[AGENTS]]"
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
  - "[[wiki/sources/2026-06-01 Using Goals in Codex]]"
  - "[[wiki/sources/2026-06-03 A harness for every task dynamic workflows in Claude Code]]"
  - "[[wiki/sources/2026-06-06 Agents that remember]]"
tags:
  - llm-wiki/concept
  - glossary
  - harness-engineering
---
# Agent Harness 术语表

本页用于统一 wiki 中保留的核心英文名词。后续整理资料时，正文默认中文；英文术语第一次出现或不易懂时，优先采用“英文术语（中文解释）”或“中文解释（English Term）”的写法。

| 英文术语 | 中文解释 | 说明 |
|---|---|---|
| Agent | 智能体 | 能读取上下文、调用工具、执行任务并根据反馈继续行动的 AI 系统。 |
| Coding Agent | 编程智能体 | 面向代码仓库工作的智能体，通常能读写文件、运行命令、测试、提交修改。 |
| Harness | 智能体工作支架 / 运行环境 | 模型之外帮助智能体可靠工作的上下文、工具、约束、流程、反馈和状态管理。 |
| Harness Engineering | 智能体工作支架工程 | 设计和改进 harness 的工程实践，使智能体更可控、可验证、可持续工作。 |
| Outer Harness | 用户侧外层工作支架 | 用户或团队围绕现有 agent 产品额外搭建的规则、文档、脚本、检查器和反馈环。 |
| Feedforward Guides | 生成前引导 | 在智能体开始生成前提供的原则、规则、参考文档、示例、CLI、codemod 等。 |
| Feedback Sensors | 生成后反馈检测器 | 在智能体产出后检测问题并反馈的机制，如测试、lint、日志、浏览器检查、review agent。 |
| Sensor | 检测器 / 反馈探针 | 用于观察结果或环境状态，并把问题反馈给智能体或人类的工具或流程。 |
| Computational Control | 计算型控制 | 由程序确定性执行的控制，如类型检查、lint、单测、结构测试。 |
| Inferential Control | 推断型控制 | 依赖 LLM 或语义判断的控制，如 review agent、LLM-as-judge。 |
| Middleware | 中间件 / 调用拦截层 | 插在模型调用、工具调用或 agent loop 中间的可编程逻辑，用于注入上下文、改写请求或拦截行为。 |
| Trace | 执行轨迹 | 一次智能体运行中的输入、工具调用、输出、错误和中间状态记录。 |
| Trace-driven Iteration | 基于执行轨迹的迭代 | 通过分析失败 trace 找到 agent/harness 问题，再定向改进。 |
| Build-Verify Loop | 构建-验证循环 | 智能体先实现，再运行测试/端到端检查/用户视角验证，失败则修复并重试。 |
| Context Injection | 上下文注入 | harness 主动把目录结构、规则、工具说明、验收标准等加入智能体上下文。 |
| Reasoning Budgeting | 推理预算分配 | 在规划、实现、验证等阶段分配不同的思考深度、时间或 token 预算。 |
| Session Handoff | 跨会话交接 | 通过进度文件、git history、任务清单等外化状态，让下一个会话能接着做。 |
| Compaction | 上下文压缩 | 将长对话或长任务状态压缩成较短摘要，避免超过上下文窗口。 |
| Sandbox | 沙箱 | 限制智能体可访问资源和可执行操作的隔离环境。 |
| Tool Orchestration | 工具编排 | 安排智能体何时、如何、以什么权限调用搜索、终端、浏览器、测试等工具。 |
| Planner | 规划智能体 / 规划角色 | 负责拆解需求、确定范围、定义验收标准的角色。 |
| Generator | 生成智能体 / 实现角色 | 负责按计划生成代码、文档或其他产物的角色。 |
| Evaluator | 评估智能体 / 评审角色 | 独立检查产物质量、发现遗漏、提出修复建议的角色。 |
| Sprint Contract | 短周期交付契约 | 实现前协商好的“完成定义”、可测试行为和验收边界。 |
| Feature List | 功能清单 | 明确要实现/验证的功能列表，可作为测试契约或进度追踪依据。 |
| Progress File | 进度文件 | 跨 session 记录当前状态、已做事项、剩余问题和下一步的文件。 |
| System of Record | 权威记录系统 | 团队约定的事实来源；在本 wiki 语境中常指版本化仓库或 wiki。 |
| Mechanized Invariants | 机械化不变量 | 用测试、lint、结构规则等自动机制强制保持的架构或质量约束。 |
| Harnessability | 可支架化程度 | 一个代码库/系统被 harness 有效引导、检测和约束的难易程度。 |
| NLAH | 自然语言智能体工作支架 | Natural-Language Agent Harnesses；用自然语言文档描述 run-level harness policy。 |
| IHR | 智能工作支架运行时 | Intelligent Harness Runtime；解释 NLAH 并执行 agent calls、handoffs、state updates、validation gates、artifact contracts。 |
| Harness Policy Layer | 工作支架策略层 | 适合自然语言表达的角色、契约、证据、重试、验证、交接和停止条件。 |
| Artifact Contract | 产物契约 | 对 agent run 应产出什么证据/文件/状态以及何时可完成的约束。 |
| File-backed State | 文件承载状态 | 把关键任务状态写入文件系统，便于后续步骤、子 agent 或新 session 读取。 |
| Harness Module Ablation | 工作支架模块消融 | 在共享 runtime 下增删 harness module，评估其对 performance、成本、handoff 等指标的影响。 |
| Agent Loop | 智能体循环 | 模型提出下一步/工具调用，harness 执行并返回结果的循环。 |
| Sandboxing | 沙箱隔离 | 限制 agent 工具调用能访问哪些文件、进程、网络或系统资源。 |
| Tool Surface | 工具界面 | agent 可见、可调用的工具集合及其抽象层级。 |
| Context Engineering | 上下文工程 | 为 agent 提供任务、文件、文档、PR 历史和工具入口，同时控制上下文体积与新鲜度。 |
| Agent Harness | 智能体工作支架 | 模型之外让智能体能行动、观察、记忆、验证和恢复的系统层；LangChain 用 Agent = Model + Harness 概括。 |
| Filesystem Primitive | 文件系统原语 | 把文件/目录/git workspace 作为 agent 的持久状态层和协作表面。 |
| Bash + Code Execution | Bash 与代码执行 | 给 agent 终端/脚本执行能力，让它临时写工具并运行代码解决问题。 |
| Context Rot | 上下文腐化 | 上下文窗口变长、变乱或充满无关内容后，模型表现下降的现象。 |
| Tool Call Offloading | 工具调用卸载 | 大型工具输出写入文件，只把摘要、头尾片段或路径放进上下文。 |
| Progressive Disclosure | 渐进披露 | 先暴露轻量能力摘要，任务需要时再加载完整技能/工具说明，以减少上下文噪声。 |
| Ralph Loop | Ralph 循环 | 拦截 agent 退出，在干净上下文中重新注入目标并读取文件状态继续工作的 harness pattern。 |
| Model-Harness Co-evolution | 模型-支架共演化 | harness primitive 进入产品和后训练循环后，模型更擅长使用该 harness，同时可能过拟合工具协议。 |
| Claude Code Hooks | Claude Code 事件钩子 | 在工具调用前后、停止、压缩、权限通知等事件触发的自动化。 |
| Subagent | 子智能体 | 主 agent 可委派的有限职责/有限工具/有限权限 agent 角色。 |
| MCP | 模型上下文协议 | Model Context Protocol；把外部服务能力暴露给 agent 的协议/服务器体系。 |
| Plugin | 插件 | 打包 skills、MCP、hooks 或工具的可安装单元。 |
| Tool Budget | 工具预算 | 在上下文和性能约束下可启用的 MCP/plugin/tool 数量与描述规模。 |
| Worktree | Git 工作树 | 同一仓库的独立 checkout，用于并行 agent 工作隔离。 |
| Codemap | 代码地图 | 帮助 agent 快速理解目录、模块、入口和变更位置的导航文件。 |
| Goal | 目标 | Codex thread 上的持久完成契约，记录 objective、status、budget 和 evidence checks。 |
| Completion Contract | 完成契约 | 说明最终状态、验证面、约束、边界、迭代策略和阻塞停止条件。 |
| Verification Surface | 验证面 | 用来证明目标完成的测试、benchmark、日志、文件、artifact 或研究材料。 |
| Continuation Gate | 继续门控 | 判断 Goal 是否可自动继续的安全边界，如 thread idle、无 queued input、within budget。 |
| Evidence-Based Completion | 证据驱动完成 | 只有具体证据支持目标达成时才标记完成。 |
| Dynamic Workflow | 动态工作流 | Claude Code 中由 Claude 为当前任务现场生成/执行的 JavaScript 多智能体 workflow。 |
| Task-specific Harness | 面向任务的定制支架 | 围绕当前任务风险、结构、验证和资源约束动态组织的 harness。 |
| Agentic Laziness | 智能体懒惰 | 智能体在复杂多部分任务中只做部分进展就提前宣称完成。 |
| Self-preferential Bias | 自我偏好偏差 | 智能体在验证或评价时过度相信自己的输出。 |
| Goal Drift | 目标漂移 | 长任务或 compaction 后，原始目标、边缘约束或负约束逐步丢失。 |
| Fan-out-and-synthesize | 分发并综合 | 并行处理多个子任务，再在 barrier step 合并结构化输出。 |
| Adversarial Verification | 对抗式验证 | 用独立 verifier agent 按 rubric 挑错和验证结果。 |
| Tournament | 锦标赛式比较 | 多个 agent 竞争完成同一任务，再通过 pairwise judging 筛出赢家。 |
| Quarantine | 隔离区 | 处理不可信内容的 agent 不直接执行高权限动作，由可信执行角色隔离处理。 |
| Memory Store | 记忆存储 | 挂载到 agent session 的持久文件系统式状态层，用于跨 session 保存和读取记忆。 |
| Dreaming | 记忆整理 / 梦境整理 | 异步读取历史 sessions 和 memory store，去重、核查、补充并生成新 memory store 的多智能体流程。 |
| Output Memory Store | 输出记忆存储 | Dreaming 生成的新 store；input store 不被直接修改，方便 review 和切换。 |
| Memory Version | 记忆版本 | memory store 中每次变更产生的不可变版本记录，用于审计、恢复和 redaction。 |
| Read-only Memory | 只读记忆 | 允许 agent 读取但不写入的 memory store access mode，适合共享参考资料或不可信输入场景。 |
