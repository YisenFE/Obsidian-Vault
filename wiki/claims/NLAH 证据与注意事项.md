---
type: claim-set
status: draft
created: 2026-05-29
updated: 2026-05-29
aliases:
  - Natural-language harness evidence and caveats
sources:
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
tags:
  - llm-wiki/claim
  - harness-engineering
  - natural-language-harness
---
# NLAH 证据与注意事项

## 范围

本页追踪 [[wiki/sources/2026-05-28 Natural-Language Agent Harnesses|Natural-Language Agent Harnesses]] 中关于 NLAH/IHR 可行性、机制可审计性、模块消融和风险边界的主要论断。

## 来源支持的论断

| 论断 | 来源证据 | 状态 |
|---|---|---|
| 自然语言可以承载 run-level harness policy，并由共享 runtime 执行。 | RQ1 中 NLAH+IHR 在 Live-SWE、MHTBA/TB2、OSWorld/SeeAct 上达到与 code/prompt realization 同量级表现。 | 来源支持；未独立复现 |
| NLAH 的核心优势不只是分数，而是让 policy layer 可读、可比较、可 ablate。 | 表 2 显示静态 policy materials 大幅缩短；论文强调 separation of policy and deterministic mechanisms。 | 来源支持 |
| IHR 能把 policy 物化为可观测机制。 | RQ2 中 artifact contract、tool call success、failed tool continuation 指标较高，显示 contracts、tools、recovery 被执行。 | 来源支持 |
| Handoff 是当前 IHR prototype 的主要弱点。 | RQ2 显示 NLAH 在 Orchestration Reliability 和 Information Handoff Recall 上低于 Prompt，尤其 parent-child handoff recall 下降明显。 | 来源支持 |
| 显式模块可消融，且 state/evidence/acceptance discipline 比单纯增加分支更有效。 | RQ3 中 file-backed state、self-evolution、evidence-backed answering 正向；multi-candidate search 增加 agent calls 但 SWE 得分下降；context compression 负向。 | 来源支持 |
| NLAH 不应被理解为自然语言替代所有 controller code。 | 附录讨论明确说自然语言适合 policy，代码仍适合 parsers、tool execution、sandboxing、adapters、logging、validators。 | 来源支持 |

## 注意事项 / 局限

- 实验未由本 wiki 复现；所有分数、token 和 call metrics 都按论文报告记录。
- Prompt baseline 在 Live-SWE 与 MHTBA 上高于 IHR-executed NLAH，因此 IHR 价值需要从可审计、可执行语义和模块实验角度理解。
- IHR prototype 有额外模型/工具调用和 token 开销，工程效率仍待优化。
- Handoff recall 是关键瓶颈，可能影响长时程、多子 agent、跨 session 任务。
- 论文提醒 portable harness logic 可能带来 prompt injection、malicious tool grafting、supply-chain contamination 等风险，需要 provenance、review、permission control 和 sandbox。
- 论文中的 `gpt-5.4-mini`、Codex CLI 版本、benchmark setting 均作为来源内实验设定记录，不代表本 wiki 对这些外部产品状态做独立确认。

## 后续待验证问题

| 问题 | 为什么重要 | 状态 |
|---|---|---|
| NLAH 在真实团队仓库中的收益是否高于普通 `AGENTS.md` + skills？ | 这关系到 NLAH 是否只是研究 representation，还是可落地工程范式。 | 待验证 |
| IHR handoff recall 如何提升？ | 低 handoff recall 会限制多 agent 和长任务可靠性。 | 待验证 |
| NLAH 安全审查应如何做？ | 可移植 harness policy 可能携带危险工具调用或隐藏的 workflow 风险。 | 待验证 |
| 哪些 NLAH modules 可迁移到本 vault 的 Obsidian ingest/query 工作流？ | 可能改进长期 wiki 维护，但需要避免过度工程化。 | 待验证 |

## 相关页面

- [[wiki/concepts/Natural-Language Agent Harnesses|Natural-Language Agent Harnesses]]
- [[wiki/concepts/Intelligent Harness Runtime|Intelligent Harness Runtime]]
- [[wiki/concepts/Harness Policy Layer|Harness Policy Layer]]
- [[wiki/concepts/Harness Module Ablation|Harness Module Ablation]]
- [[wiki/concepts/File-backed State|File-backed State]]
