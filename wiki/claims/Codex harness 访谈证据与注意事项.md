---
type: claim-set
status: draft
created: 2026-05-29
updated: 2026-05-29
aliases:
  - Codex harness interview evidence and caveats
sources:
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
tags:
  - llm-wiki/claim
  - codex
  - harness-engineering
  - interview
---
# Codex harness 访谈证据与注意事项

## 范围

本页追踪 Michael Bolin 访谈中关于 Codex harness、sandboxing、安全边界、tool surface、agent-first workflow 和 context engineering 的主要论断，并标注它们作为访谈来源的证据边界。

## 来源支持的论断

| 论断 | 来源证据 | 状态 |
|---|---|---|
| Codex harness 是 agent loop：给模型上下文和工具，执行 tool calls，再把结果返回模型。 | 1:20 起 Bolin 直接定义 harness / agent loop。 | 来源支持 |
| Codex harness 对 sandboxing/security 极其重视。 | 2:08 起 Bolin 说明 Codex 会把 shell/computer-use commands 放入 sandbox 或用户 policy；2:53 起列举 macOS/Linux/Windows 机制。 | 来源支持 |
| Security 与 safety 应区分。 | 3:24 起 Bolin 解释 security 是读写哪些 folder 等权限边界，safety 更多发生在模型后端侧。 | 来源支持 |
| Codex 倾向 small/tight harness 和少量强工具。 | 15:38 起 Bolin 说 Codex 尽量让 harness small and tight；16:09 起说明不给 explicit read-file tool，而是给 terminal。 | 来源支持 |
| Agent-first 开发让文档、测试、架构和 `AGENTS.md` 更重要。 | 10:13 起 Bolin 说文档、TDD 等旧 best practices 在 agent-first world 更明显值得；11:04 起说明 Codex 团队使用 modest `AGENTS.md`。 | 来源支持的判断 |
| 多 agent 并行提升吞吐，但带来新的 workstream management。 | 6:51 起 Bolin 说 throughput 是最大变化之一，并自述多 repo clone 并行。 | 个人经验陈述 |
| Sandboxing 在 coding tasks 中可替代频繁 human-in-the-loop。 | 17:49 起 Bolin 说对其关注的 coding tasks，sandboxing 是很多场景下 human-in-the-loop 的替代机制。 | 来源支持，但需按风险场景限定 |

## 注意事项 / 局限

- 该来源是访谈，不是受控实验；大多数结论是产品团队经验和设计哲学。
- 用量增长、VS Code 超过 CLI、Codex app 受欢迎等说法来自访谈自述，未在本 wiki 独立验证。
- 访谈解释了 sandbox 设计方向，但没有给出完整 threat model 或安全审计结果。
- “少量强工具”与“NLAH 可执行 policy”可能代表不同 harness 取向，需要后续综合比较。
- “sandboxing 替代 human-in-the-loop”只应理解为某些 coding tasks 的吞吐优化，不应外推到高风险生产操作。

## 后续待验证问题

| 问题 | 为什么重要 | 状态 |
|---|---|---|
| Codex open-source repo 中 sandbox 实现与访谈描述是否完全一致？ | 需要代码审计才能确认实际 security boundary。 | 待验证 |
| Small tool surface 是否在 benchmark 或真实团队中优于多专用工具？ | 这是 Codex 与其他 agent harness 的关键架构差异。 | 待验证 |
| Modest `AGENTS.md` 的最佳长度和内容边界是什么？ | 直接影响本 vault / repo 级 agent 指南设计。 | 待验证 |
| 多 agent workstream 如何避免 context switching 与 review overload？ | 访谈强调吞吐，但也承认这是新的 inner loop，需要优化。 | 待验证 |

## 相关页面

- [[wiki/concepts/Agent Loop|Agent Loop]]
- [[wiki/concepts/Sandbox and Tool Orchestration|Sandbox and Tool Orchestration]]
- [[wiki/concepts/Small Powerful Tool Surface|Small Powerful Tool Surface]]
- [[wiki/concepts/Context Engineering for Coding Agents|Context Engineering for Coding Agents]]
- [[wiki/entities/products/Codex|Codex]]
