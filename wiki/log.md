---
type: log
status: active
created: 2026-05-28
updated: 2026-05-29
tags:
  - llm-wiki/log
---
# Wiki 日志

追加式记录。新记录写在顶部或底部都可以，但不要改写历史记录；建议使用统一标题格式，方便 grep：

```md
## [YYYY-MM-DD] ingest | Source Title
## [YYYY-MM-DD] query | Question Title
## [YYYY-MM-DD] lint | Scope
```

## [2026-05-29] schema | 中文写作与术语解释规范

- 更新 [[AGENTS]]：要求 `wiki/` 正文默认中文，核心英文术语首次出现时给中文解释。
- 将现有 wiki/template 的常用英文段落标题改为中文。
- 更新模板，新增“术语说明”段，避免后续整理时出现整段英文或难懂英文名词无解释。
- 新增 [[wiki/concepts/Agent Harness 术语表]]，统一常见英文术语的中文解释。

## [2026-05-28] setup | Karpathy LLM Wiki structure

- 按 [[Karpathy wiki 方法论]] 建立三层结构：`raw/`、`wiki/`、`AGENTS.md`。
- 保留现有 `raw/*.md` 原始资料不动。
- 创建初始目录：`wiki/sources/`、`wiki/concepts/`、`wiki/entities/`、`wiki/themes/`、`wiki/questions/`、`wiki/syntheses/`、`wiki/claims/`、`wiki/outputs/`、`templates/`。
- 在 [[wiki/index]] 登记当前 raw 来源，状态均为 `raw-only`，等待逐篇 ingest。

## [2026-05-28] ingest | 工程技术：在智能体优先的世界中利用 Codex

- 读取 [[raw/2026-05-28 工程技术：在智能体优先的世界中利用 Codex]]，并为两张外部图示新增本地资产：[[raw/assets/2026-05-28-codex-devtools-mcp.webp]]、[[raw/assets/2026-05-28-codex-observability-stack.webp]]。
- 创建来源摘要：[[wiki/sources/2026-05-28 工程技术：在智能体优先的世界中利用 Codex]]。
- 创建/更新概念页：[[wiki/concepts/Harness Engineering]]、[[wiki/concepts/Codex-first Development]]、[[wiki/concepts/Agent-readable Codebase]]、[[wiki/concepts/Repository as System of Record]]、[[wiki/concepts/Mechanized Invariants]]。
- 创建主题/论断页：[[wiki/themes/智能体优先软件开发]]、[[wiki/themes/智能体熵与垃圾回收]]、[[wiki/claims/Codex-first 工程证据与注意事项]]。
- 创建实体页：[[wiki/entities/people/Ryan Lopopolo]]、[[wiki/entities/people/Victor Zhu]]、[[wiki/entities/people/Zach Brock]]、[[wiki/entities/organizations/OpenAI]]、[[wiki/entities/products/Codex]]、[[wiki/entities/products/Aardvark]]、[[wiki/entities/products/Chrome DevTools MCP]]。
- 更新 [[wiki/index]] 与 [[wiki/overview]]，把该来源状态改为 `ingested` 并登记新页面。
- 待确认：raw frontmatter 的 `published: 2026-05-27` 与正文/官网日期 2026-02-11 冲突；本次未改 raw 文本，只在 wiki 中标记为待验证。


## [2026-05-28] fix | 修正 Codex 文章发布时间元数据

- 根据用户确认，修正 [[raw/2026-05-28 工程技术：在智能体优先的世界中利用 Codex]] frontmatter：`published` 从 `2026-05-27` 改为 `2026-02-11`。
- 同步更新 [[wiki/sources/2026-05-28 工程技术：在智能体优先的世界中利用 Codex]]、[[wiki/claims/Codex-first 工程证据与注意事项]] 与 [[wiki/overview]] 中关于日期冲突/待验证的说明。

## [2026-05-29] ingest | Effective harnesses for long-running agents

- 读取 [[raw/2026-05-28 Effective harnesses for long-running agents]]，并为外部 GIF 图示新增本地资产：[[raw/assets/2026-05-28-anthropic-long-running-agents-puppeteer.gif]]。
- 创建来源摘要：[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]。
- 创建概念页：[[wiki/concepts/Agent Memory and Session Handoff]]、[[wiki/concepts/Feature List as Test Contract]]、[[wiki/concepts/Self-verification]]。
- 更新概念页：[[wiki/concepts/Harness Engineering]]、[[wiki/concepts/Agent-readable Codebase]]、[[wiki/concepts/Repository as System of Record]]、[[wiki/concepts/Mechanized Invariants]]。
- 创建主题/论断页：[[wiki/themes/长时程智能体工作流]]、[[wiki/claims/长时程 agent harness 证据与注意事项]]。
- 创建实体页：[[wiki/entities/people/Justin Young]]、[[wiki/entities/organizations/Anthropic]]、[[wiki/entities/products/Claude Agent SDK]]、[[wiki/entities/products/Claude Code]]、[[wiki/entities/products/Puppeteer MCP]]。
- 更新 [[wiki/index]] 与 [[wiki/overview]]，把该来源状态改为 `ingested` 并登记新页面。
- 待确认：raw frontmatter 缺失 `author` 与 `published`；wiki 中作者取自正文，发布日期取自官方页面，本次未改 raw 文本。

## [2026-05-29] ingest | Harness design for long-running application development

- 读取 [[raw/2026-05-28 Harness design for long-running application development]]，并从官方页面补充作者/发布日期元数据：作者 [[wiki/entities/people/Prithvi Rajasekaran]]，发布日期 2026-03-24；raw frontmatter 未改。
- 下载并查看外部媒体资产：[[raw/assets/2026-05-28-harness-design-solo-retro-game-maker.png]]、[[raw/assets/2026-05-28-harness-design-full-retro-game-maker.webp]]、[[raw/assets/2026-05-28-harness-design-dutch-museum.mp4]]、[[raw/assets/2026-05-28-harness-design-dutch-museum-frame-24s.jpg]]、[[raw/assets/2026-05-28-harness-design-browser-daw.mp4]]、[[raw/assets/2026-05-28-harness-design-browser-daw-frame.jpg]]。
- 创建来源摘要：[[wiki/sources/2026-05-28 Harness design for long-running application development]]。
- 创建概念页：[[wiki/concepts/Planner-Generator-Evaluator Harness]]、[[wiki/concepts/External Evaluator Agent]]、[[wiki/concepts/Sprint Contract]]、[[wiki/concepts/Load-bearing Harness Components]]、[[wiki/concepts/Context Reset vs Compaction]]。
- 更新概念/主题页：[[wiki/concepts/Harness Engineering]]、[[wiki/concepts/Agent Memory and Session Handoff]]、[[wiki/concepts/Self-verification]]、[[wiki/concepts/Feature List as Test Contract]]、[[wiki/themes/长时程智能体工作流]]、[[wiki/themes/智能体优先软件开发]]。
- 创建综合/论断页：[[wiki/syntheses/Anthropic 长时程 harness 演化]]、[[wiki/claims/Planner-generator-evaluator harness 证据与注意事项]]。
- 创建/更新实体页：[[wiki/entities/people/Prithvi Rajasekaran]]、[[wiki/entities/organizations/Anthropic]]、[[wiki/entities/products/Claude Agent SDK]]、[[wiki/entities/products/Claude Code]]、[[wiki/entities/products/Playwright MCP]]、[[wiki/entities/products/Claude Opus 4.5]]、[[wiki/entities/products/Claude Opus 4.6]]、[[wiki/entities/products/Claude Sonnet 4.5]]、[[wiki/entities/people/Justin Young]]。
- 更新 [[wiki/index]] 与 [[wiki/overview]]，把该来源状态改为 `ingested` 并登记新页面。
- 待验证：成本/时长/质量提升均为 Anthropic 自述；solo vs full harness 并非等 token/等时间对照。

## [2026-05-29] ingest | Harness engineering for coding agent users

- 读取 [[raw/2026-05-28 Harness engineering for coding agent users]]；raw frontmatter 已含作者 [[wiki/entities/people/Birgitta Böckeler]] 与发布日期 2026-04-02，本次未改 raw 文本。
- 下载并查看外部图示资产：[[raw/assets/2026-05-28-fowler-harness-bounded-contexts.png]]、[[raw/assets/2026-05-28-fowler-harness-overview.png]]、[[raw/assets/2026-05-28-fowler-harness-change-lifecycle-examples.png]]、[[raw/assets/2026-05-28-fowler-harness-types.png]]、[[raw/assets/2026-05-28-fowler-harness-templates.png]]。
- 创建来源摘要：[[wiki/sources/2026-05-28 Harness engineering for coding agent users]]。
- 创建概念页：[[wiki/concepts/Coding Agent User Harness]]、[[wiki/concepts/Feedforward Guides]]、[[wiki/concepts/Feedback Sensors]]、[[wiki/concepts/Computational and Inferential Controls]]、[[wiki/concepts/Harness Regulation Categories]]、[[wiki/concepts/Behaviour Harness]]、[[wiki/concepts/Harnessability]]、[[wiki/concepts/Harness Templates]]。
- 更新概念/主题页：[[wiki/concepts/Harness Engineering]]、[[wiki/concepts/Agent-readable Codebase]]、[[wiki/concepts/Mechanized Invariants]]、[[wiki/concepts/Self-verification]]、[[wiki/concepts/External Evaluator Agent]]、[[wiki/concepts/Repository as System of Record]]、[[wiki/themes/智能体优先软件开发]]。
- 创建综合/论断页：[[wiki/syntheses/跨来源 harness 定义综合]]、[[wiki/claims/Coding-agent 用户 harness 证据与注意事项]]。
- 创建/更新实体页：[[wiki/entities/people/Birgitta Böckeler]]、[[wiki/entities/people/Martin Fowler]]、[[wiki/entities/organizations/Thoughtworks]]、[[wiki/entities/organizations/Stripe]]、[[wiki/entities/products/ArchUnit]]、[[wiki/entities/products/OpenRewrite]]、[[wiki/entities/products/Semgrep]]、[[wiki/entities/products/Claude Code]]。
- 更新 [[wiki/index]] 与 [[wiki/overview]]，把该来源状态改为 `ingested` 并登记新页面。
- 待验证：文章是 mental model / field-practice synthesis，不是量化实验；behaviour harness、harness coverage、harness templates 的有效度仍需后续来源或实践验证。

## [2026-05-29] ingest | Improving Deep Agents with harness engineering

- 读取 [[raw/2026-05-28 Improving Deep Agents with harness engineering]]；raw frontmatter 已含作者 [[wiki/entities/people/Vivek Trivedy]] 与发布日期 2026-02-18，本次未改 raw 文本。
- 下载并查看外部图示资产：[[raw/assets/2026-05-28-langchain-terminal-bench-score.png]]、[[raw/assets/2026-05-28-langchain-baseline-score.png]]、[[raw/assets/2026-05-28-langchain-trace-analyzer-skill.png]]、[[raw/assets/2026-05-28-langchain-self-verification-loop.png]]、[[raw/assets/2026-05-28-langchain-reasoning-sandwich.png]]。
- 创建来源摘要：[[wiki/sources/2026-05-28 Improving Deep Agents with harness engineering]]。
- 创建概念页：[[wiki/concepts/Trace-driven Harness Iteration]]、[[wiki/concepts/Build-Verify Loop]]、[[wiki/concepts/Middleware Hooks]]、[[wiki/concepts/Local Context Injection]]、[[wiki/concepts/Reasoning Budgeting]]。
- 更新概念/主题页：[[wiki/concepts/Harness Engineering]]、[[wiki/concepts/Feedback Sensors]]、[[wiki/concepts/Self-verification]]、[[wiki/concepts/Load-bearing Harness Components]]、[[wiki/concepts/Behaviour Harness]]、[[wiki/themes/智能体优先软件开发]]。
- 更新综合/论断页：[[wiki/syntheses/跨来源 harness 定义综合]]；创建 [[wiki/claims/Deep Agents harness engineering 证据与注意事项]]。
- 创建/更新实体页：[[wiki/entities/people/Vivek Trivedy]]、[[wiki/entities/organizations/LangChain]]、[[wiki/entities/products/Deep Agents]]、[[wiki/entities/products/LangSmith]]、[[wiki/entities/products/Terminal Bench]]、[[wiki/entities/products/Harbor]]、[[wiki/entities/products/Daytona]]、[[wiki/entities/products/GPT-5.2-Codex]]、[[wiki/entities/organizations/OpenAI]]、[[wiki/entities/products/Claude Opus 4.6]]。
- 更新 [[wiki/index]] 与 [[wiki/overview]]，把该来源状态改为 `ingested` 并登记新页面。
- 待验证：Terminal Bench 分数、Top 5 排名和 Claude Opus 4.6 对比均为 LangChain 自述；trace-driven 优化存在 benchmark overfitting 风险。

## [2026-05-29] lint | Wiki 写作原则中文化

- 按 [[AGENTS]] 新增的中文写作与术语解释规范，对现有 `wiki/` 做批量修正。
- 将主题、综合、论断页中文化并改为中文优先命名：[[wiki/themes/智能体优先软件开发]]、[[wiki/themes/长时程智能体工作流]]、[[wiki/themes/智能体熵与垃圾回收]]、[[wiki/syntheses/跨来源 harness 定义综合]]、[[wiki/syntheses/Anthropic 长时程 harness 演化]]。
- 将论断页改为中文表头与中文说明：[[wiki/claims/Codex-first 工程证据与注意事项]]、[[wiki/claims/长时程 agent harness 证据与注意事项]]、[[wiki/claims/Planner-generator-evaluator harness 证据与注意事项]]、[[wiki/claims/Coding-agent 用户 harness 证据与注意事项]]、[[wiki/claims/Deep Agents harness engineering 证据与注意事项]]。
- 中文化来源摘要、实体页与概念页首段术语说明；保留来源标题、产品名、组织名、人名和代码标识符原文。
- 同步更新 [[wiki/index]]、[[wiki/overview]] 与内部 wikilink，验证无断链、frontmatter/YAML 正常。

## [2026-05-29] ingest | Natural-Language Agent Harnesses

- 读取 [[raw/2026-05-28 Natural-Language Agent Harnesses]]；raw frontmatter 的 `published` 为空，本次按 arXiv submission history 在 wiki 记录 v2 日期 2026-05-18，raw 未改。
- 使用 arXiv HTML/PDF 入口补充论文正文信息，并创建来源摘要：[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]。
- 创建概念页：[[wiki/concepts/Natural-Language Agent Harnesses]]、[[wiki/concepts/Intelligent Harness Runtime]]、[[wiki/concepts/Harness Policy Layer]]、[[wiki/concepts/Artifact Contract]]、[[wiki/concepts/File-backed State]]、[[wiki/concepts/Harness Module Ablation]]。
- 更新概念/综合/主题页：[[wiki/concepts/Harness Engineering]]、[[wiki/concepts/Agent Memory and Session Handoff]]、[[wiki/concepts/Context Reset vs Compaction]]、[[wiki/concepts/Self-verification]]、[[wiki/concepts/Load-bearing Harness Components]]、[[wiki/concepts/Agent Harness 术语表]]、[[wiki/syntheses/跨来源 harness 定义综合]]、[[wiki/themes/智能体优先软件开发]]。
- 创建论断页：[[wiki/claims/NLAH 证据与注意事项]]。
- 创建实体页：[[wiki/entities/people/Linyue Pan]]、[[wiki/entities/people/Lexiao Zou]]、[[wiki/entities/people/Shuo Guo]]、[[wiki/entities/people/Jingchen Ni]]、[[wiki/entities/people/Hai-Tao Zheng]]、[[wiki/entities/organizations/Tsinghua University Shenzhen International Graduate School]]、[[wiki/entities/organizations/Harbin Institute of Technology (Shenzhen)]]、[[wiki/entities/products/Codex CLI]]、[[wiki/entities/products/GPT-5.4-Mini]]、[[wiki/entities/products/SWE-bench Verified]]、[[wiki/entities/products/Live-SWE-Agent]]、[[wiki/entities/products/MHTBA]]、[[wiki/entities/products/Meta-Harness]]、[[wiki/entities/products/OSWorld]]、[[wiki/entities/products/SeeAct]]、[[wiki/entities/products/LinguaClaw]]。
- 更新 [[wiki/entities/products/Terminal Bench]]、[[wiki/index]] 与 [[wiki/overview]]，把该来源状态改为 `ingested` 并登记新页面。
- 待验证：NLAH/IHR 的 benchmark 分数、token/call metrics、module ablation 与安全边界均来自论文自述；本 wiki 未复现实验。

## [2026-05-29] ingest | OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents

- 读取 [[raw/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]；该来源为 YouTube/Turing Post transcript，raw 未改。
- 创建来源摘要：[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]。
- 创建概念页：[[wiki/concepts/Agent Loop]]、[[wiki/concepts/Sandbox and Tool Orchestration]]、[[wiki/concepts/Safety vs Security in Agentic Systems]]、[[wiki/concepts/Small Powerful Tool Surface]]、[[wiki/concepts/Context Engineering for Coding Agents]]。
- 更新概念/综合/主题页：[[wiki/concepts/Harness Engineering]]、[[wiki/concepts/Agent-readable Codebase]]、[[wiki/concepts/Coding Agent User Harness]]、[[wiki/concepts/Agent Memory and Session Handoff]]、[[wiki/concepts/Context Reset vs Compaction]]、[[wiki/concepts/Agent Harness 术语表]]、[[wiki/syntheses/跨来源 harness 定义综合]]、[[wiki/themes/智能体优先软件开发]]。
- 创建/更新实体页：[[wiki/entities/people/Michael Bolin]]、[[wiki/entities/people/Ksenia]]、[[wiki/entities/organizations/OpenAI]]、[[wiki/entities/organizations/Turing Post]]、[[wiki/entities/products/Codex]]、[[wiki/entities/products/Codex CLI]]、[[wiki/entities/products/Codex App]]、[[wiki/entities/products/GPT-5]]、[[wiki/entities/products/VS Code]]、[[wiki/entities/products/JetBrains]]、[[wiki/entities/products/Xcode]]。
- 创建论断页：[[wiki/claims/Codex harness 访谈证据与注意事项]]。
- 更新 [[wiki/index]] 与 [[wiki/overview]]，把该来源状态改为 `ingested` 并纳入当前总览。
- 待验证：访谈中的用量增长、IDE/app 时间线、sandbox 实现细节和“sandboxing 替代 frequent human-in-the-loop”均为来源自述或经验判断；本 wiki 尚未审计 Codex repo 或独立复现实验。

## [2026-05-29] ingest | The Anatomy of an Agent Harness

- 读取 [[raw/2026-05-28 The Anatomy of an Agent Harness]]；raw 文本未改。
- 下载并查看外部图示资产：[[raw/assets/2026-05-28-langchain-agent-harness-behavior-design.png]]、[[raw/assets/2026-05-28-langchain-agent-harness-terminal-bench.png]]。
- 创建来源摘要：[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]。
- 创建概念页：[[wiki/concepts/Agent Harness]]、[[wiki/concepts/Filesystem as Harness Primitive]]、[[wiki/concepts/Bash and Code Execution]]、[[wiki/concepts/Context Rot]]、[[wiki/concepts/Tool Call Offloading]]、[[wiki/concepts/Skills as Progressive Disclosure]]、[[wiki/concepts/Ralph Loop]]、[[wiki/concepts/Model-Harness Co-evolution]]。
- 更新概念/综合/主题页：[[wiki/concepts/Harness Engineering]]、[[wiki/concepts/Agent Loop]]、[[wiki/concepts/Sandbox and Tool Orchestration]]、[[wiki/concepts/Small Powerful Tool Surface]]、[[wiki/concepts/Context Engineering for Coding Agents]]、[[wiki/concepts/Context Reset vs Compaction]]、[[wiki/concepts/File-backed State]]、[[wiki/concepts/Self-verification]]、[[wiki/concepts/Load-bearing Harness Components]]、[[wiki/concepts/Agent Memory and Session Handoff]]、[[wiki/concepts/Trace-driven Harness Iteration]]、[[wiki/concepts/Agent Harness 术语表]]、[[wiki/syntheses/跨来源 harness 定义综合]]、[[wiki/themes/智能体优先软件开发]]、[[wiki/themes/长时程智能体工作流]]。
- 更新实体页：[[wiki/entities/people/Vivek Trivedy]]、[[wiki/entities/organizations/LangChain]]、[[wiki/entities/products/Deep Agents]]、[[wiki/entities/products/Terminal Bench]]、[[wiki/entities/products/Codex]]、[[wiki/entities/products/Claude Code]]。
- 创建论断页：[[wiki/claims/Agent harness anatomy 证据与注意事项]]。
- 更新 [[wiki/index]] 与 [[wiki/overview]]，把该来源状态改为 `ingested` 并移出下一步待 ingest 列表。
- 待验证：文章是概念框架而非受控实验；Terminal Bench、Codex/Claude Code 后训练、apply_patch tool logic overfitting 等外部论断均未独立复现或审计。

## [2026-06-01] ingest | The Shorthand Guide to Everything Claude Code

- 读取 [[raw/2026-06-01 The Shorthand Guide to Everything Claude Code]]；raw 文本未改。
- 下载并查看外部图片/视频 poster 资产：[[raw/assets/2026-06-01-claude-code-shorthand-01-hero-setup.jpg]]、[[raw/assets/2026-06-01-claude-code-shorthand-02-command-chaining.jpg]]、[[raw/assets/2026-06-01-claude-code-shorthand-03-posttooluse-hook-feedback.png]]、[[raw/assets/2026-06-01-claude-code-shorthand-04-supabase-mcp-tables.jpg]]、[[raw/assets/2026-06-01-claude-code-shorthand-05-plugins-mcp-status.jpg]]、[[raw/assets/2026-06-01-claude-code-shorthand-06-mixedbread-grep-marketplace.jpg]]、[[raw/assets/2026-06-01-claude-code-shorthand-07-tmux-video-poster.jpg]]、[[raw/assets/2026-06-01-claude-code-shorthand-08-github-actions-pr-review.jpg]]、[[raw/assets/2026-06-01-claude-code-shorthand-09-zed-command-palette.jpg]]、[[raw/assets/2026-06-01-claude-code-shorthand-10-vscode-extension-docs.jpg]]、[[raw/assets/2026-06-01-claude-code-shorthand-11-custom-statusline.jpg]]。
- 创建来源摘要：[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]。
- 创建概念页：[[wiki/concepts/Claude Code Operating Harness]]、[[wiki/concepts/Claude Code Hooks]]、[[wiki/concepts/Subagent Scoping]]、[[wiki/concepts/MCP and Plugin Context Budget]]、[[wiki/concepts/Parallel Agent Workflows]]、[[wiki/concepts/Agent Rules and Memory]]、[[wiki/concepts/Codemaps for Agents]]。
- 更新概念/综合/主题页：[[wiki/concepts/Coding Agent User Harness]]、[[wiki/concepts/Skills as Progressive Disclosure]]、[[wiki/concepts/Middleware Hooks]]、[[wiki/concepts/Context Rot]]、[[wiki/concepts/Context Engineering for Coding Agents]]、[[wiki/concepts/Feedforward Guides]]、[[wiki/concepts/Feedback Sensors]]、[[wiki/concepts/Mechanized Invariants]]、[[wiki/concepts/Agent-readable Codebase]]、[[wiki/concepts/Agent Memory and Session Handoff]]、[[wiki/concepts/Sandbox and Tool Orchestration]]、[[wiki/concepts/Self-verification]]、[[wiki/concepts/Agent Harness 术语表]]、[[wiki/syntheses/跨来源 harness 定义综合]]、[[wiki/themes/智能体优先软件开发]]、[[wiki/themes/长时程智能体工作流]]。
- 创建/更新实体页：[[wiki/entities/people/affaan]]、[[wiki/entities/organizations/Anthropic]]、[[wiki/entities/products/Claude Code]]、[[wiki/entities/products/Model Context Protocol]]、[[wiki/entities/products/Zed]]、[[wiki/entities/products/VS Code]]、[[wiki/entities/products/Cursor]]、[[wiki/entities/products/tmux]]、[[wiki/entities/products/mgrep]]、[[wiki/entities/products/hookify]]、[[wiki/entities/products/Supabase]]、[[wiki/entities/products/GitHub Actions]]。
- 创建论断页：[[wiki/claims/Claude Code shorthand 证据与注意事项]]。
- 更新 [[wiki/index]] 与 [[wiki/overview]]，登记该来源并纳入当前总览。
- 待确认：raw frontmatter 的 `published: 2025-09-16` 与 X status id 推断日期 2026-01-17 不一致，且正文中 2025-09-16 更像引用的 hackathon 帖日期；本次未改 raw。
- 待验证：MCP/tool budget 数字、Claude Code 版本/插件市场状态、MCP/plugin 安全性和 hook/subagent 最佳实践均为个人经验或来源时点陈述。

## [2026-06-01] fix | 修正 Claude Code shorthand 发布时间元数据

- 根据用户确认，修正 [[raw/2026-06-01 The Shorthand Guide to Everything Claude Code]] frontmatter：`published` 从 `2025-09-16` 改为 `2026-01-17`。
- 修正依据：源 X status id `2012378465664745795` 推断发布时间为 2026-01-17 UTC；raw 正文中的 `2025年9月16日` 是引用的 Anthropic x Forum Ventures hackathon 帖日期，正文保留不改。
- 同步更新 [[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]] 与 [[wiki/claims/Claude Code shorthand 证据与注意事项]] 中的待确认说明。

## [2026-06-01] ingest | Using Goals in Codex

- 读取 [[raw/2026-06-01 Using Goals in Codex]]；raw 文本未改。
- 下载并查看外部图示资产：[[raw/assets/2026-06-01-codex-goals-01-goal-continuation-loop.png]]、[[raw/assets/2026-06-01-codex-goals-02-goal-thread-state.png]]、[[raw/assets/2026-06-01-codex-goals-03-goal-dispatcher-conditions.png]]、[[raw/assets/2026-06-01-codex-goals-04-strong-goal-components.png]]、[[raw/assets/2026-06-01-codex-goals-05-research-evidence-channels.png]]、[[raw/assets/2026-06-01-codex-goals-06-research-support-levels.png]]、[[raw/assets/2026-06-01-codex-goals-07-goal-final-output.png]]。
- 创建来源摘要：[[wiki/sources/2026-06-01 Using Goals in Codex]]。
- 创建概念页：[[wiki/concepts/Codex Goals]]、[[wiki/concepts/Goal Completion Contract]]、[[wiki/concepts/Goal Lifecycle and Continuation Gates]]、[[wiki/concepts/Evidence-Based Completion]]、[[wiki/concepts/Research Goal Audit]]。
- 更新概念/综合/主题页：[[wiki/concepts/Artifact Contract]]、[[wiki/concepts/Self-verification]]、[[wiki/concepts/Agent Loop]]、[[wiki/concepts/Agent Memory and Session Handoff]]、[[wiki/concepts/Context Engineering for Coding Agents]]、[[wiki/concepts/Agent Harness 术语表]]、[[wiki/syntheses/跨来源 harness 定义综合]]、[[wiki/themes/智能体优先软件开发]]。
- 更新实体页：[[wiki/entities/organizations/OpenAI]]、[[wiki/entities/products/Codex]]、[[wiki/entities/products/Codex CLI]]。
- 创建论断页：[[wiki/claims/Codex Goals 证据与注意事项]]。
- 更新 [[wiki/index]] 与 [[wiki/overview]]，登记该来源并纳入当前总览。
- 待验证：raw frontmatter 的 author 字段像剪藏误抽取，published 为空；Codex 0.128.0、Goals 命令表面、预算策略和 lifecycle 行为可能随产品版本变化。

## [2026-06-03] ingest | A harness for every task: dynamic workflows in Claude Code

- 读取 [[raw/2026-06-03 A harness for every task dynamic workflows in Claude Code]]；raw 文本未改。
- 使用 Claude blog 外部页面核对元数据：发表日期为 2026-06-02，作者为 [[wiki/entities/people/Thariq Shihipar]] 与 [[wiki/entities/people/Sid Bidasaria]]；raw frontmatter 的 `published: 2001-06-02` 记录为待确认剪藏元数据错误，未直接修正 raw。
- 创建来源摘要：[[wiki/sources/2026-06-03 A harness for every task dynamic workflows in Claude Code]]。
- 创建概念页：[[wiki/concepts/Dynamic Workflows]]、[[wiki/concepts/Long-running Agent Failure Modes]]。
- 更新概念/主题/综合页：[[wiki/concepts/Agent Harness]]、[[wiki/concepts/Harness Engineering]]、[[wiki/concepts/Claude Code Operating Harness]]、[[wiki/concepts/Parallel Agent Workflows]]、[[wiki/concepts/Subagent Scoping]]、[[wiki/concepts/Agent Rules and Memory]]、[[wiki/concepts/Self-verification]]、[[wiki/concepts/External Evaluator Agent]]、[[wiki/concepts/Context Reset vs Compaction]]、[[wiki/concepts/Agent Harness 术语表]]、[[wiki/themes/长时程智能体工作流]]、[[wiki/syntheses/Anthropic 长时程 harness 演化]]。
- 创建/更新实体页：[[wiki/entities/people/Thariq Shihipar]]、[[wiki/entities/people/Sid Bidasaria]]、[[wiki/entities/organizations/Anthropic]]、[[wiki/entities/products/Claude Code]]、[[wiki/entities/products/Claude Agent SDK]]、[[wiki/entities/products/Claude Opus 4.8]]、[[wiki/entities/products/Bun]]。
- 创建论断页：[[wiki/claims/Claude Code dynamic workflows 证据与注意事项]]。
- 更新 [[wiki/index]] 与 [[wiki/overview]]，登记该来源并纳入当前总览。
- 待验证：dynamic workflows 的质量提升、token 成本、恢复语义、quarantine 权限隔离、Bun 迁移案例和 Claude Code 产品细节均为来源时点陈述；外部图示未下载到 `raw/assets/`。

## [2026-06-05] ingest | Agents that remember

- 读取 [[raw/2026-06-06 Agents that remember]]；raw 文本未改。
- 使用 Claude API Docs 的 agent memory / dreams 页面与 Claude blog 的 Managed Agents 发布文章补充核对 memory stores、dreaming、research preview、权限和版本审计等产品细节。
- 创建来源摘要：[[wiki/sources/2026-06-06 Agents that remember]]。
- 创建概念页：[[wiki/concepts/Agent Memory Stores]]、[[wiki/concepts/Dreaming for Agent Memory]]。
- 更新概念/主题/综合页：[[wiki/concepts/Agent Memory and Session Handoff]]、[[wiki/concepts/File-backed State]]、[[wiki/concepts/Context Reset vs Compaction]]、[[wiki/concepts/Harness Engineering]]、[[wiki/concepts/Dynamic Workflows]]、[[wiki/concepts/Agent Harness 术语表]]、[[wiki/themes/长时程智能体工作流]]、[[wiki/syntheses/Anthropic 长时程 harness 演化]]。
- 创建/更新实体页：[[wiki/entities/organizations/Anthropic]]、[[wiki/entities/products/Claude Managed Agents]]、[[wiki/entities/products/Claude Platform]]、[[wiki/entities/products/Claude Opus 4.7]]、[[wiki/entities/products/Claude Sonnet 4.6]]、[[wiki/entities/products/Claude Opus 4.8]]。
- 创建论断页：[[wiki/claims/Claude Managed Agents memory 与 dreaming 证据与注意事项]]。
- 更新 [[wiki/index]] 与 [[wiki/overview]]，登记该来源并纳入当前总览。
- 待验证：speaker Kevin 的全名、dreaming 的 token/cost 预期、95% cache hit rate、质量提升、API/Console 细节、read-write memory store 的实际安全防线；raw 文件名/frontmatter `created: 2026-06-06` 与本地 ingest 日期 2026-06-05 不一致，raw 未改。

## [2026-06-06] query | Claude Code 有必要使用 memory store 和 dreaming 吗

- 基于 [[wiki/concepts/Agent Memory Stores]]、[[wiki/concepts/Dreaming for Agent Memory]]、[[wiki/concepts/Claude Code Operating Harness]] 和 [[wiki/concepts/Agent Rules and Memory]]，沉淀判断：Claude Code 日常编码优先使用 `CLAUDE.md`、auto memory、rules、skills、hooks、subagents、dynamic workflows 和测试验证；memory store / dreaming 更适合 Claude Managed Agents 或平台托管、跨 session、可审计长期记忆场景。
- 创建问题页：[[wiki/questions/Claude Code 有必要使用 memory store 和 dreaming 吗]]。
