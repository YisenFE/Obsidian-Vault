# LLM Wiki Obsidian Vault

这是一个按 Karpathy wiki 方法论维护的 Obsidian 知识库，当前主题集中在智能体工作支架（Agent Harness）、智能体工作支架工程（Harness Engineering）、Codex-first development、长时程智能体工作流、Claude Code / Codex / LangChain / Anthropic 相关实践，以及可执行自然语言 harness。

本 vault 的核心目标不是保存原文剪藏，而是把原始资料持续转化为可查询、可演化、可追溯的中文知识层。

## 快速入口

- [AGENTS.md](AGENTS.md)：LLM 维护本 vault 时必须遵守的 schema、目录规范和工作流。
- [Karpathy wiki 方法论.md](Karpathy\ wiki\ 方法论.md)：本知识库三层模型的方法论来源。
- [wiki/index.md](wiki/index.md)：wiki 内容目录，ingest 或 query 前优先阅读。
- [wiki/overview.md](wiki/overview.md)：当前领域总览、高层判断、研究边界和后续问题。
- [wiki/log.md](wiki/log.md)：追加式操作日志。

## 目录结构

```text
raw/
  inbox/        # 临时放入、尚未整理的新资料
  assets/       # 本地图片、PDF、网页附件等
  *.md          # 原始资料层，原则上只读

wiki/
  index.md      # 内容目录
  log.md        # 追加式操作日志
  overview.md   # 当前领域总览
  sources/      # 每个 raw 来源对应的 LLM 摘要页
  concepts/     # 概念页
  entities/     # 人物、组织、产品、项目、工具
  themes/       # 横向主题页
  questions/    # 有长期价值的问题和答案
  syntheses/    # 多来源综合、比较和判断
  claims/       # 重要论断、证据链、冲突和待验证项
  outputs/      # slides、charts 等输出产物

templates/      # LLM 复制使用的页面模板
```

## 三层模型

1. `raw/` 是原始资料层。用于保存剪藏、论文、访谈、图片、视频和附件，原则上不在 ingest 中改写。
2. `wiki/` 是 LLM 维护的知识层。摘要、概念、实体、主题、问题、综合分析和 claims 都在这里持续演化。
3. `AGENTS.md` 是操作规范。每次 ingest、query、lint 都先遵守这里定义的 schema 和流程。

## 当前内容范围

已整理内容主要覆盖：

- OpenAI / Codex-first engineering / Codex Goals
- Anthropic 长时程 agents 与 planner-generator-evaluator harness
- MartinFowler.com / Thoughtworks 风格的 coding-agent 用户侧 harness engineering
- LangChain 的 Deep Agents、Terminal Bench、trace-driven harness iteration 和 Agent = Model + Harness 论述
- Natural-Language Agent Harnesses（NLAH）与 Intelligent Harness Runtime（IHR）
- Claude Code 的 skills、hooks、subagents、rules/memory、MCP/plugins、worktrees、tmux 等个人 operating harness 实践

更完整的主题状态以 [wiki/index.md](wiki/index.md) 和 [wiki/overview.md](wiki/overview.md) 为准。

## 维护约定

- `wiki/` 正文默认使用中文；核心英文术语可以保留，但首次出现时应给出中文解释。
- 优先使用 Obsidian 双链，例如 `[[wiki/concepts/Agent Harness]]`。
- 每篇 wiki 页面尽量包含 YAML frontmatter：`type`、`status`、`created`、`updated`、`sources`、`tags`。
- 来源支持的结论、推断和待验证项要区分清楚。
- 多来源冲突写入 `wiki/claims/`，或写入相关页面的“冲突 / 待验证”段落。
- 新增或更新 wiki 页面后，同步更新 `wiki/index.md`；重要操作追加到 `wiki/log.md`，不要重写旧日志。

## 常用工作流

### Ingest 新来源

1. 读取对应 `raw/` 文件；如有图片、PDF 或视频，必要时一起查看。
2. 在 `wiki/sources/` 创建或更新来源摘要页，使用 [templates/source-summary.md](templates/source-summary.md)。
3. 抽取并更新相关概念页、实体页、主题页和论断页。
4. 更新 `wiki/index.md` 和必要的 `wiki/overview.md`。
5. 向 `wiki/log.md` 追加 `## [YYYY-MM-DD] ingest | Source Title` 记录。

### Query 知识库

1. 先读 `wiki/index.md`，再读相关 wiki 页面。
2. 必要时回到 `raw/` 查证原始资料。
3. 回答中明确区分来源支持的结论、推断和待验证项。
4. 如果答案有长期价值，沉淀到 `wiki/questions/` 或 `wiki/syntheses/`，并更新索引与日志。

### Lint 知识库

定期检查孤立页面、重复概念、断链、未建实体页、遗漏索引，以及新来源是否推翻旧结论。

## 给维护者的提醒

- 不要把 `raw/` 当作可编辑草稿区；它是事实来源。
- 不要把未 ingest 的 raw 内容直接合成为长期结论。
- 不确定内容标记为 `待验证`，不要伪装成结论。
- 写作时优先让页面可被 Obsidian 浏览、可被 LLM 检索、可被后续维护者继续演化。
