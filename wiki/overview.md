---
type: overview
status: evolving
created: 2026-05-28
updated: 2026-06-03
sources:
  - "[[Karpathy wiki 方法论]]"
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
  - "[[wiki/sources/2026-06-03 A harness for every task dynamic workflows in Claude Code]]"
tags:
  - llm-wiki/overview
---
# 总览

本 wiki 当前围绕智能体工作支架（agent harness）、智能体工作支架工程（harness engineering）、Codex-first development、长时程 agent、coding-agent 用户侧 harness、基于执行轨迹的 harness 迭代、可执行自然语言 harness representation，以及 Claude Code dynamic workflows 展开。已 ingest 的来源包括 OpenAI、Anthropic、MartinFowler.com / Birgitta Böckeler、LangChain、arXiv NLAH 论文、Michael Bolin 的 Codex 访谈、LangChain 的 agent harness anatomy、Claude Code 用户侧配置实践、Codex Goals 指南与 Claude Code dynamic workflows 官方文章。

## 当前高层判断

- **智能体优先开发的瓶颈是 harness，而不只是模型能力。** OpenAI 来源把工程师重心转向环境、意图、工具、约束和反馈回路；Anthropic 来源落到跨 session handoff 和多 agent 分工；Böckeler 来源把用户侧 outer harness 明确为 guides + sensors；LangChain 一方面展示如何用 traces 和 benchmark 迭代 harness knobs，另一方面用 Agent = Model + Harness 梳理 filesystem、bash、sandbox、context management、verification 等基础 primitive；NLAH 论文进一步把 harness policy 变成可执行、可审计、可消融的对象；Michael Bolin 访谈则从 Codex builder 角度强调 small/tight harness、sandboxing 与少量强工具。
- **Agent = Model + Harness 是有用但过宽的起点。** LangChain Anatomy 用它说明模型智能必须通过 harness 变成工作能力；但进入具体讨论时仍要区分 model/builder harness、项目/团队 operating harness、coding-agent user harness、harness improvement loop、harness representation layer 五层。见 [[wiki/syntheses/跨来源 harness 定义综合|跨来源 harness 定义综合]]。
- **文件系统、bash、sandbox 是底层运行面。** LangChain Anatomy 把 filesystem + git、bash/code execution、sandbox/default tooling 视为从“模型只能输出文本”到“agent 能实际工作”的基础桥梁；这也解释了为什么 Codex 的 terminal-first 与 sandbox-first 取向如此重要。
- **代码仓库正在变成智能体的可读世界模型。** `AGENTS.md` 更像目录而不是手册；真正知识进入版本化 docs、计划、架构、质量记录、progress file、feature list、sprint contract、guides/sensors 配置、git history 和可执行启动脚本。
- **工具预算是上下文工程的一部分。** Claude Code shorthand 来源提醒：配置很多 MCP/plugins 不等于全部启用；active tools 会消耗上下文窗口、增加选择复杂度和延迟。
- **上下文管理不只是压缩。** Context rot 的缓解手段包括 compaction、tool call offloading、skills/progressive disclosure 和 file-backed state；NLAH 的负向 compression ablation 也提示压缩不能替代可审计状态。
- **长时程 agent 需要显式交接。** Context compaction 有帮助但不足够；每个新 context/window 或 agent 阶段都需要读取上一轮留下的 progress、commit、feature contract、evaluator log 和基础验证结果。NLAH 论文的 IHR handoff weakness 也从 shared runtime 角度支持这一点。
- **用户侧 harness 已经细化到个人操作系统。** Claude Code shorthand 来源展示了更具体的一层：skills/commands 负责复用流程，hooks 负责自动反馈，subagents 负责范围限定，rules/memory 负责长期偏好，MCP/plugins 负责能力扩展，worktrees/tmux/editor/statusline 负责并行隔离和可观察性。
- **Claude Code dynamic workflows 把 harness 变成按任务生成。** 新来源说明 Claude Code 可以执行 JavaScript workflow，动态 spawn subagents、选择模型和 worktree 隔离，并组合 fan-out、adversarial verification、tournament、loop-until-done 等模式；它更适合复杂、高价值、长时程或对抗性任务，而不是所有 coding task 的默认解法。
- **长任务失败模式正在被显式命名。** Dynamic workflows 来源把 agentic laziness、自我偏好偏差和 goal drift 作为单上下文复杂任务的核心风险；这把 completion contract、external evaluator、file-backed state、clean context 和 workflow synthesis 的价值连接得更清楚。
- **Feedforward + feedback 是用户侧 harness 的核心。** 生成前引导（feedforward guides）提高首次生成正确率；生成后反馈检测器（feedback sensors）把问题尽量留在 agent 自修正、人类 review、pipeline、连续健康监控或 trace-driven improvement loop 中。
- **自然语言适合承载 harness policy，但不应替代所有代码。** NLAH 论文把 roles、contracts、evidence、validation、handoff 和 stopping conditions 放进自然语言文档；parser、tool execution、sandbox、adapter、logging、validator 仍应由代码层承担。
- **Codex 访谈提供了 small-tool-surface 取向。** Bolin 倾向让 harness 尽量小而紧，给 agent 少量强工具（例如 terminal）和足够 sandbox backstop，而不是为每个操作都做专用 wrapper。
- **Trace 与 explicit module 是 harness 外循环的重要反馈。** LangChain 用 traces 找失败模式；NLAH 论文用 module ablation 比较 file-backed state、self-evolution、evidence-backed answering、multi-candidate search、context compression 等模块是否承重。
- **完成契约正在产品化。** Codex Goals 把目标、验证面、约束、边界、迭代策略、阻塞停止条件、预算和 lifecycle 放进 thread-scoped state，使“继续直到证据说完成”成为产品能力。
- **“完成”必须绑定验证证据，但 behaviour harness 仍最弱。** 维护性和架构 fitness 有较多 deterministic tooling；功能行为仍依赖清晰 spec、测试质量、人工判断和更成熟的 behaviour sensors。NLAH 的 artifact contract 和 evidence-backed answering 是把完成绑定到证据的另一种表达。
- **高吞吐需要机械边界和 middleware guardrails。** 自定义 lint、结构测试、不可随意改写的 feature list、sprint contract、codemods、pre-completion checklist、loop detection 和 time-budget warnings 都是在把人类判断或环境约束转成可执行控制。
- **Agent-first developer inner loop 也需要被设计。** Bolin 访谈强调，开发者会管理多个 parallel workstreams、把重复流程沉淀为 skills、让 Codex 参与 code review；这使人类工作从单线写代码转向调度与优化多 agent 工作流。
- **计算化控制优先，推断式控制补位。** Computational controls 快、确定、便宜；inferential controls 能做语义/品味判断；middleware/IHR 这类 runtime 则可以在 agent loop 的关键节点确定性注入二者产生的信号。
- **模型和 harness 会共演化。** 有用 primitive 会被加入产品并进入后训练循环，模型会更擅长使用该 harness；但这也带来 tool-protocol overfitting 和 benchmark 跨 harness 可比性问题。
- **Harness 组件会随模型和代码库能力移动。** Context reset、sprint decomposition、external evaluator、middleware hooks、reasoning budget、file-backed state、context compression 是否承重，取决于模型能力、任务边界、代码库 harnessability、质量目标、成本和延迟。
- **许多结论仍是来源自述或论文实验。** OpenAI 的量化指标、Anthropic 的质量提升、LangChain 的 Terminal Bench 改进、Böckeler 的 harnessability/templates 预测、NLAH 的 benchmark 与 module ablation 都需独立复现或跨来源验证。

## 当前边界

- 原始资料在 `raw/`；除新增本地媒体资产用于读取图示/视频外，未改写 raw 文本。
- `wiki/` 会逐篇 ingest 并演化综合，不提前把未处理来源合成为结论。
- 当前综合主要来自 OpenAI、Anthropic、MartinFowler.com/Thoughtworks 风格来源、LangChain、Michael Bolin 访谈、Claude Code 第三方用户实践、Claude Code 官方 dynamic workflows 文章与 NLAH arXiv 论文。
- 两篇 Anthropic 来源的 raw frontmatter 缺失 `author`/`published`；wiki 中作者来自正文，发布日期来自官方页面，raw 未改动。NLAH raw frontmatter 的 `published` 为空，本 wiki 记录 arXiv v2 日期，raw 未改。
- Claude Code dynamic workflows raw frontmatter 的 `published: 2001-06-02` 与外部页面 2026-06-02 不一致；wiki 按外部页面记录，raw 未改。

## 初始研究问题

1. 不同作者/组织如何定义 “agent harness”？
2. 长时程 agent 能稳定工作的关键机制是什么？
3. 用户侧 harness 与平台/产品侧 harness 的边界在哪里？
4. Codex、Claude Agent SDK、LangChain 的设计取向有何差异？
5. 哪些机制是可迁移到个人/团队工作流中的实践？
6. 智能体优先开发中，哪些量化指标可信、可复现、可迁移？
7. Session handoff、repository-as-system-of-record 与长期 memory store 之间如何分层？
8. 如何判断一个 harness 组件是否真正 load-bearing？
9. 外部 evaluator 的 criteria 如何校准，才能严格但不过拟合某个人的偏好？
10. Harness coverage / harness quality 应如何度量？
11. Behaviour harness 如何减少对 AI 生成测试和人工测试的过度依赖？
12. Trace-driven harness iteration 如何避免 benchmark overfitting？
13. Reasoning budget、time budget 和 latency/cost 之间如何做系统性权衡？
14. NLAH、`AGENTS.md`、skills 与 workflow DSL 的边界在哪里？
15. 可执行自然语言 harness 如何做 provenance、权限、沙箱和供应链安全审查？
16. Dynamic workflows 与 static workflows、skills、subagents、hooks 的复用边界在哪里？
17. 对抗验证和 tournament workflow 的 token 成本、false positives 与质量提升如何量化？

## 下一步建议

1. 创建 “Codex vs Claude Agent SDK vs LangChain vs NLAH/IHR” 综合页，对比 repo operating environment、session handoff、多 agent evaluator、trace/middleware optimization、small tool surface、自然语言 policy runtime、filesystem/bash/sandbox primitive。
2. 对各 claims 页做二次核验，特别是 OpenAI 自述指标、Anthropic 成本/质量对比、LangChain Terminal Bench 分数、NLAH benchmark 与 module ablation。
3. 继续追踪 model-harness co-evolution：哪些 primitive 会被模型吸收，哪些仍需系统层显式实现。
4. 把 Claude Code shorthand 的个人配置经验抽象成团队级最小 harness checklist，并验证 MCP/tool budget。
5. 把 Codex Goals 的 completion contract 模板迁移到 wiki ingest / research audit / code review 等长任务。
6. 把 Claude Code dynamic workflow patterns 抽象成可选模板，并记录哪些任务确实需要额外 compute。
