---
type: question
status: draft
created: 2026-06-06
updated: 2026-06-06
sources:
  - "[[wiki/concepts/Agent Memory Stores]]"
  - "[[wiki/concepts/Dreaming for Agent Memory]]"
  - "[[wiki/concepts/Claude Code Operating Harness]]"
  - "[[wiki/concepts/Agent Rules and Memory]]"
  - "[[wiki/sources/2026-06-06 Agents that remember]]"
  - "[[wiki/sources/2026-06-03 A harness for every task dynamic workflows in Claude Code]]"
tags:
  - llm-wiki/question
  - claude-code
  - agent-memory
  - managed-agents
---
# Claude Code 有必要使用 memory store 和 dreaming 吗

## 简短回答

对 Claude Code 日常编码来说，通常不需要把 Claude Managed Agents 的 memory store 和 dreaming 当成必需能力。更合理的默认做法是先用 Claude Code 自己的本地记忆和操作支架：`CLAUDE.md`、auto memory、rules、skills、hooks、subagents、git worktree、动态工作流和可验证测试。

Memory store 和 dreaming 更适合平台托管 agent、跨 session 自动执行、团队级长期知识沉淀，或者需要把很多历史 session 统一整理成可审计 memory store 的场景。

## 适合使用的情况

- 同一个 agent 要长期服务多个用户、项目或团队，并且需要跨 session 自动记住用户偏好、项目约定、历史错误和领域知识。
- 任务不是单个 repo 的一次性修改，而是平台侧 managed agent workflow，需要 API/Console 管理 memory、权限、版本和审计。
- 历史 session 很多，memory 已经出现重复、过时、冲突或结构混乱，需要 dreaming 做异步整理并产出新的 output memory store。
- 需要区分 shared reference store、personal store、project store，并对不同 store 设置 `read_only` / `read_write` 权限。

## 不值得上的情况

- 只是用 Claude Code 在本地 repo 里写代码、跑测试、做 review。
- 规则可以稳定写进 `CLAUDE.md`、项目 rules、skills、hooks、lint/test 或文档。
- 记忆内容能被 git history、issue、PR、README、测试或当前代码直接恢复。
- 团队还没有明确 memory owner、review 流程和污染防线；此时 read-write memory store 可能把 prompt injection、错误事实或临时偏好带进未来 session。

## 对 Claude Code 的建议

优先把长期规则放在 repo 可审计位置：项目级 `CLAUDE.md` / rules 记录稳定约定，hook/lint/test 承担硬约束，skills/commands 承担可复用流程，dynamic workflows 承担大规模并行或对抗验证任务。

如果未来需要把 Claude Code 接入 Claude Managed Agents 或自建类似平台，再考虑 memory store；当 memory store 开始膨胀或冲突时，再引入 dreaming。不要为了“有记忆”而先上 dreaming，它解决的是长期记忆质量维护问题，不是 Claude Code 日常上下文不足的第一解。

## 待验证

- Claude Code 与 Claude Managed Agents 的产品边界可能继续变化；具体可用性、计划权限和 API 细节应以官方文档当前版本为准。
- Claude Code auto memory 与 Claude Managed Agents memory store 在团队协作、云端环境和审计能力上的边界需要持续观察。
