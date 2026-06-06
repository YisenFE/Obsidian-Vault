---
type: claim-set
status: draft
created: 2026-06-05
updated: 2026-06-05
aliases:
  - Claude Managed Agents memory and dreaming evidence and caveats
sources:
  - "[[wiki/sources/2026-06-06 Agents that remember]]"
tags:
  - llm-wiki/claim
  - managed-agents
  - agent-memory
  - dreaming
  - anthropic
---
# Claude Managed Agents memory 与 dreaming 证据与注意事项

## 范围

本页追踪 Agents that remember workshop 及官方 docs 对 Claude Managed Agents memory stores 与 dreaming 的主要论断：跨 session 记忆、filesystem interface、访问权限、版本审计、异步 memory consolidation、多智能体 dreaming harness、非破坏性 output store、成本和安全边界。

## 来源支持的论断

| 论断 | 来源证据 | 状态 |
|---|---|---|
| 默认 session 是隔离的，不能自然跨 session 共享所学信息。 | workshop 演示先告诉一个 session 新信息，再创建另一个 session 提问，后者无法回忆。 | 来源支持 |
| Memory store 通过文件系统式 mount 让 agent 跨 session 读写记忆。 | workshop 说明 memory store mount 到 session container，agent 可用 bash/grep/read files；官方 docs 也说明其挂载在 sandbox 目录。 | 来源 + docs 支持 |
| Memory store 不是单一全局记忆，应按 owner/scope/lifecycle 切分。 | workshop 提到可 per user/per workspace 等；docs 建议 focused stores，并支持多个 stores/session。 | 来源 + docs 支持 |
| Dreaming 是维护 memory 质量的后台 multi-agent harness。 | workshop 说明 dream job 异步运行，读取 memory store 和 transcripts，orchestrator 派 subagents，做 fact-check/enrich/dedupe/organize。 | 来源支持 |
| Dreaming 非破坏性，适合 review 后切换。 | workshop 和 docs 均说明 input store 不被修改，dream 产生 separate output memory store，可 review/discard。 | 来源 + docs 支持 |
| Dreaming 更像 memory maintenance，而不只是 memory storage。 | workshop 强调 memory 会无界增长、重复、过时；dreaming 负责整理和保持高信号。 | 来源支持 |
| Write access 是安全边界。 | 官方 docs 明确提示处理不可信输入时 read-write memory store 可能被 prompt injection 污染，未来 session 会把它当可信 memory 读入。 | docs 支持 |
| Dreaming 会有明显 token 成本，但可通过 cache/model/instructions/budget 控制。 | workshop Q&A 提到 exhaustive by design、95% cache hit rate 预期、模型选择、prompt steering 和 token budget；docs 暴露 usage 与 supported models。 | 来源自述，待验证 |

## 注意事项 / 局限

- Workshop 是产品/开发者演示，不是 controlled benchmark；对质量、成本、检索效率的提升需要具体业务验证。
- Raw transcript 中 “45 minutes” 与实际 transcript 时间约 28 分钟不一致，可能来自剪藏描述或视频元数据差异。
- Speaker 只标为 Kevin at Anthropic，未核实全名；本 wiki 暂不创建人物实体页。
- Dreaming 在官方 docs 中为 research preview；API beta header、模型支持和限制可能变化。
- Memory store 是文件系统式接口，这提升 agent 可用性，也扩大了写入污染、权限分层、审计和 redaction 的设计责任。
- Workshop 中的 95% cache hit rate 是来源自述，本 wiki 未复验。

## 后续待验证问题

| 问题 | 为什么重要 | 状态 |
|---|---|---|
| Memory store 分层的最佳实践是什么？ | 影响跨用户/团队/项目共享时的污染和权限风险。 | 待验证 |
| Dreaming 应在什么频率和输入规模下运行？ | 影响成本、延迟和整理质量。 | 待验证 |
| Dreaming 产出的 output store 如何做 human review？ | 非破坏性只有配合 review/rollback 才有治理价值。 | 待验证 |
| Memory store 与 repo/docs/rules 的职责边界在哪里？ | 避免同一事实散落到 memory、AGENTS.md、CLAUDE.md 和 progress file。 | 待验证 |
| Prompt injection 写入 memory 的防线是什么？ | 一次污染可能跨 session 放大。 | 待验证 |

## 相关页面

- [[wiki/concepts/Agent Memory Stores|Agent Memory Stores]]
- [[wiki/concepts/Dreaming for Agent Memory|Dreaming for Agent Memory]]
- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]]
- [[wiki/concepts/File-backed State|File-backed State]]
- [[wiki/entities/products/Claude Managed Agents|Claude Managed Agents]]
