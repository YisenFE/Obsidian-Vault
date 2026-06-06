---
type: source-summary
status: ingested
created: 2026-06-05
updated: 2026-06-05
source: "[[raw/2026-06-06 Agents that remember]]"
external_url: "https://www.youtube.com/watch?v=geUv4CjPpxI&list=PLmWCw1CzcFinm44PAkEoR2glf-iNPhulP&index=5"
author: "Claude YouTube channel; speaker Kevin at Anthropic (full name 待验证)"
published: 2026-05-23
tags:
  - llm-wiki/source
  - managed-agents
  - agent-memory
  - dreaming
  - harness-engineering
---
# Agents that remember

## 一句话结论

这场 Claude workshop 把 agent 记忆拆成三层：session 是临时执行实例，memory store（记忆存储）把信息以文件系统形式跨 session 持久化，dreaming（记忆整理/梦境整理）则用异步多智能体 harness 从旧 transcript 和现有记忆中核查、去重、补充细节并产出新的可审查 memory store。

## 来源元数据

- 原始资料：[[raw/2026-06-06 Agents that remember]]
- 外部链接：[YouTube — Agents that remember](https://www.youtube.com/watch?v=geUv4CjPpxI&list=PLmWCw1CzcFinm44PAkEoR2glf-iNPhulP&index=5)
- 发布方/作者：Claude YouTube channel；主讲人为 Anthropic 工程师 Kevin（全名待验证）
- 发表时间：2026-05-23
- 补充核对：Claude API Docs 的 [Using agent memory](https://platform.claude.com/docs/en/managed-agents/memory) 与 [Dreams](https://platform.claude.com/docs/en/managed-agents/dreams)，以及 Claude blog 的 [New in Claude Managed Agents](https://claude.com/blog/new-in-claude-managed-agents)。
- 日期注意：本地 ingest 日期使用 `date +%F` 的 2026-06-05；raw 文件名/frontmatter 的 `created: 2026-06-06` 未改。

## 关键要点

1. 默认 agent session 彼此隔离：一个 session 中告诉 agent 的信息，不会自然传到另一个 session。
2. [[wiki/concepts/Agent Memory Stores|Memory store]] 是 attached to session 的持久文件系统式资源，agent 可以跨 session 读写；可以按用户、团队、项目或 workspace 划定边界。
3. Memory store 被 mount 到 session container 中，agent 可以用文件工具、bash、grep 等熟悉的 filesystem primitive 检索和写入记忆。
4. 创建 session 时可以挂载 memory store，并配置 instructions/prompt 约束 agent 应记什么，也可以配置 `read_write` 或 `read_only` 访问权限。
5. Memory 文件可由 API/Console 列出、读取、编辑和版本化；人类可以手动补充、修正或审查记忆。
6. 单纯让 agent 写 memory 会带来新问题：agent 可能持续 dump 信息，导致 memory store 无界增长、重复、过时、结构混乱。
7. [[wiki/concepts/Dreaming for Agent Memory|Dreaming]] 是异步 background job：读取 input memory store 和历史 session transcripts，运行多智能体 harness 做 fact-check、enrich、dedupe、organize，并写入 output memory store。
8. Dreaming 是非破坏性的：不会直接修改 input memory store，而是 clone/生成新的 output memory store，方便人类 review、切换使用或丢弃。
9. Dreaming harness 使用 orchestrator + subagents；workshop 说明可按 input session 派一个 subagent，使整理过程 exhaustive by design。
10. Dreaming 产物通常会包含 index file、事件/项目 logistics、带 slug 和 metadata 的记忆文件，让未来 session 更快检索。
11. Sessions、memory stores、dreaming 可看作三层：session 负责执行，memory store 负责跨 session 连接，dreaming 负责长期整理和质量维护。
12. 成本边界：dreaming 为了 exhaustive 会用很多 tokens，但来源称大部分 token 可 cache，并可通过模型选择、prompt steering 和 token budget 控制成本。

## 术语说明

- Session（会话）：一次 agent 执行/对话实例，通常是临时的，默认结束后状态不保留给后续 session。
- Memory Store（记忆存储）：Claude Managed Agents 中可挂载到 session 的持久文件系统式存储，用于跨 session 保存偏好、项目约定、历史错误和领域上下文。
- Dreaming（记忆整理/梦境整理）：异步整理流程，读取旧 memory store 与 session transcripts，生成去重、补充、更新后的 output memory store。
- Output Memory Store（输出记忆存储）：dream job 产生的新 memory store；input store 不被直接修改。
- Read-only / Read-write Access（只读/读写权限）：memory store 挂载时的访问模式；不可信输入场景应谨慎开放写权限。
- Memory Version（记忆版本）：memory store 中文件变化的不可变版本记录，用于审计和恢复。

## 需要更新的概念

- [[wiki/concepts/Agent Memory Stores|Agent Memory Stores]]
- [[wiki/concepts/Dreaming for Agent Memory|Dreaming for Agent Memory]]
- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]]
- [[wiki/concepts/File-backed State|File-backed State]]
- [[wiki/concepts/Context Reset vs Compaction|Context Reset vs Compaction]]
- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Dynamic Workflows|Dynamic Workflows]]
- [[wiki/concepts/Agent Harness 术语表|Agent Harness 术语表]]

## 需要更新的实体

- 组织：[[wiki/entities/organizations/Anthropic|Anthropic]]
- 产品/平台：[[wiki/entities/products/Claude Managed Agents|Claude Managed Agents]]、[[wiki/entities/products/Claude Platform|Claude Platform]]、[[wiki/entities/products/Claude Opus 4.7|Claude Opus 4.7]]、[[wiki/entities/products/Claude Sonnet 4.6|Claude Sonnet 4.6]]
- 人物：Kevin（Anthropic 工程师，speaker；全名待验证，暂不建实体页）

## 论断 / 证据

| 论断 | 证据 | 置信度 |
|---|---|---:|
| Agent 默认 session 隔离会限制真实工作流，因为信息不会自然跨 session 传递。 | workshop 先演示告诉一个 session 信息，再问另一个 session，后者无法回忆。 | 高：来源演示支持 |
| Memory store 用 filesystem interface 比抽象记忆 API 更适合 agent。 | 主讲说明 memory store mount 到 session container，agent 可用 bash/grep/read files 等熟悉工具探索。官方 docs 也称 memory store 挂载为 sandbox 目录。 | 高：来源 + docs 支持 |
| Dreaming 是维护 memory store 质量的第二层机制，而不是简单长期存储。 | workshop 说明 raw memory 会重复、过时、无界增长；dreaming 负责 fact-check、enrich、dedupe、organize。 | 高：来源直接陈述 |
| Dreaming 的非破坏性 output store 适合 human-in-the-loop review。 | workshop 强调 input store 不被改，dream job 写 output store；Console 显示 diff，用户可检查是否采用。 | 高：来源支持 |
| Memory/dreaming 的价值依赖权限和范围设计。 | 来源提到 memory store 可 per user/workspace/org；官方 docs 补充 read-only/read-write、最多 8 个 stores/session、prompt injection 写入风险。 | 中高：docs 支持，具体最佳实践需验证 |
| Dreaming 成本可由 cache、模型选择、instructions 和 budget 控制。 | workshop Q&A 提到 95% cache hit rate 预期、模型选择、prompt steering、token budget；docs 也给出 supported models 和 async progress usage。 | 中：来源自述，未独立核验 |

## 冲突 / 注意事项

- Raw description 称 workshop 45 分钟，但 transcript 结束在约 28 分钟；可能是剪藏描述或视频/活动元数据差异。
- Raw author frontmatter 为 `Claude` wiki-link 形式，本文记录为 Claude YouTube channel；speaker 只出现 first name Kevin，未创建人物实体页。
- Workshop 中多处把 “Claude Managed Agents” 转写成 “cloud manage agents”；wiki 采用官方 docs canonical name。
- Memory store 是 powerful interface，也会带来安全风险：如果 read-write store 接收不可信输入，prompt injection 可能污染未来 session 的可信记忆。此点来自官方 docs 补充核对。
- Dreaming 目前按 docs 为 research preview；workshop 中的模型、CLI、Console 和 API 形态可能随 Claude Platform 版本变化。
- Raw 文件名/frontmatter `created: 2026-06-06` 与本地 ingest 日期 2026-06-05 不一致；raw 未改。

## 后续问题

- Memory store 的边界应按 user、team、workspace、project 还是 task domain 设计？
- 哪些 memory 应 read-only，哪些可以 read-write？
- Dreaming 产出的 output store 应如何 review、rollback、archive 或替换原 store？
- File-backed memory 与 repo 内 `AGENTS.md` / `CLAUDE.md` / progress file 的边界在哪里？
- 如何检测 memory store 已经变脏、过时、互相冲突，必须触发 dreaming？
