---
type: source-summary
status: ingested
created: 2026-05-29
updated: 2026-05-29
source: "[[raw/2026-05-28 Natural-Language Agent Harnesses]]"
external_url: https://arxiv.org/abs/2603.25723
author:
  - "[[wiki/entities/people/Linyue Pan|Linyue Pan]]"
  - "[[wiki/entities/people/Lexiao Zou|Lexiao Zou]]"
  - "[[wiki/entities/people/Shuo Guo|Shuo Guo]]"
  - "[[wiki/entities/people/Jingchen Ni|Jingchen Ni]]"
  - "[[wiki/entities/people/Hai-Tao Zheng|Hai-Tao Zheng]]"
published: 2026-05-18
tags:
  - llm-wiki/source
  - arxiv
  - harness-engineering
  - natural-language-harness
---
# Natural-Language Agent Harnesses

## 一句话结论

这篇 arXiv 论文把 harness（智能体工作支架/运行环境）从“嵌在 controller code 里的 glue logic”提升为可执行的自然语言对象：[[wiki/concepts/Natural-Language Agent Harnesses|Natural-Language Agent Harnesses]]（NLAH）描述 run-level harness policy，[[wiki/concepts/Intelligent Harness Runtime|Intelligent Harness Runtime]]（IHR）把这些文档解释成 agent calls、handoffs、state updates、validation gates 与 [[wiki/concepts/Artifact Contract|artifact contracts]]。

## 来源元数据

- 原始资料：[[raw/2026-05-28 Natural-Language Agent Harnesses]]
- 外部链接：[arXiv:2603.25723](https://arxiv.org/abs/2603.25723)；[HTML v2](https://arxiv.org/html/2603.25723v2)；[PDF](https://arxiv.org/pdf/2603.25723)
- 作者：[[wiki/entities/people/Linyue Pan|Linyue Pan]]、[[wiki/entities/people/Lexiao Zou|Lexiao Zou]]、[[wiki/entities/people/Shuo Guo|Shuo Guo]]、[[wiki/entities/people/Jingchen Ni|Jingchen Ni]]、[[wiki/entities/people/Hai-Tao Zheng|Hai-Tao Zheng]]
- 版本：v1 于 2026-03-26 提交；v2 于 2026-05-18 提交。raw frontmatter 的 `published` 为空，本页按 arXiv submission history 记录 v2 日期，未改 raw。
- 学科：Computation and Language；Artificial Intelligence。
- 复现包：来源附录称代码开源于 `https://github.com/curated-skills/LinguaClaw`。

## 关键要点

1. 论文的问题意识是：agent performance 强烈受 harness 影响，但现有 harness 逻辑常埋在 tightly coupled controller code 中，难以检查、比较、迁移和做 ablation。
2. [[wiki/concepts/Natural-Language Agent Harnesses|NLAH]] 是可编辑文档，负责描述 run-level harness policy：角色、契约、证据要求、retry rules、validation strategy、state handoff 和 stopping conditions。
3. [[wiki/concepts/Intelligent Harness Runtime|IHR]] 是共享运行时，负责把 NLAH 文档解释为 agent calls、handoffs、state updates、validation gates 与 artifact contracts；论文明确不是主张自然语言替代所有 controller code。
4. 作者区分 policy 与 mechanism：自然语言适合表达目标、证据、gate 和交接策略；代码仍适合 parser、tool execution、sandboxing、benchmark adapters、logging 和 deterministic validators。
5. 实验使用同一 IHR 实例：Codex CLI 0.123.0、模型 `gpt-5.4-mini`、reasoning effort `xhigh`，在 Docker 容器内运行。
6. RQ1 显示 NLAH+IHR 在三个 setting 中表现与 code/prompt realization 同量级：Live-SWE 上 NLAH 73.0，高于 code 67.0、低于 prompt 77.0；MHTBA/TB2 上 NLAH 53.9，低于 prompt 57.3、显著高于 code 36.0；OSWorld/SeeAct 上 NLAH 46.3，接近 code 47.1 与 prompt 47.9。
7. NLAH 也暴露成本问题：当前 IHR prototype 往往使用更多 model calls、tool calls 或 tokens；论文把它解释为 general agent substrate 与自然语言 orchestration 的工程开销，而非表示方式不可用。
8. 简洁性审计是该论文最强的 representation-level 结果之一：Live-SWE 可读 harness policy 从 60.1k token 的 code materials 降到 2.9k-token NLAH；MHTBA 从 10.5k 降到 0.8k；OSWorld/SeeAct 从 47.5k 降到 1.4k。
9. RQ2 显示 IHR-executed NLAH 能 materialize contracts、tools 和 recovery：Live-SWE NLAH 的 Artifact Contract 为 1.000，Tool Call Success 为 0.933，Failed Tool Continuation 为 0.992；MHTBA 对应值为 0.955、0.928、0.995。
10. 主要机制弱点是 handoff：NLAH 的 Orchestration Reliability 低于 Prompt，Information Handoff Recall 在 parent-child execution 下显著下降；论文把这视为 IHR 需要改进的具体瓶颈。
11. RQ3 显示显式 NLAH modules 可以 ablate。最有用的模块通常能强化 state 与 acceptance discipline：file-backed state 在 SWE 与 OSWorld 均提升，self-evolution 与 evidence-backed answering 也整体正向。
12. 负面结果同样重要：multi-candidate search 显著增加 agent calls，却在 SWE 上从 73.0 降到 71.4；context compression 在 SWE 与 OSWorld 都伤害 performance，说明“更多分支/更多压缩”不等于更好的 harness。
13. 论文把 NLAH 视为“harness representation science”的起点：一旦 harness 变成显式对象，就可以检索、组合、变异、优化，并研究到底是哪种 harness policy 造成差异。

## 术语说明

- Natural-Language Agent Harnesses（自然语言智能体工作支架）：用可编辑自然语言文档描述 run-level harness policy。
- Intelligent Harness Runtime（智能工作支架运行时）：解释 NLAH 文档并执行 agent calls、handoffs、state updates、validation gates、artifact contracts 的共享运行时。
- Harness Policy Layer（工作支架策略层）：角色、契约、证据、重试、验证、交接和停止条件等可读策略；与底层确定性机制分离。
- Artifact Contract（产物契约）：运行应产出的文件、证据或验收工件，以及这些工件与完成判断的关系。

## 需要更新的概念

- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Natural-Language Agent Harnesses|Natural-Language Agent Harnesses]]
- [[wiki/concepts/Intelligent Harness Runtime|Intelligent Harness Runtime]]
- [[wiki/concepts/Harness Policy Layer|Harness Policy Layer]]
- [[wiki/concepts/Artifact Contract|Artifact Contract]]
- [[wiki/concepts/File-backed State|File-backed State]]
- [[wiki/concepts/Harness Module Ablation|Harness Module Ablation]]
- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]]
- [[wiki/concepts/Context Reset vs Compaction|Context Reset vs Compaction]]
- [[wiki/concepts/Self-verification|Self-verification]]
- [[wiki/concepts/Load-bearing Harness Components|Load-bearing Harness Components]]

## 需要更新的实体

- 人物：[[wiki/entities/people/Linyue Pan|Linyue Pan]]、[[wiki/entities/people/Lexiao Zou|Lexiao Zou]]、[[wiki/entities/people/Shuo Guo|Shuo Guo]]、[[wiki/entities/people/Jingchen Ni|Jingchen Ni]]、[[wiki/entities/people/Hai-Tao Zheng|Hai-Tao Zheng]]
- 组织：[[wiki/entities/organizations/Tsinghua University Shenzhen International Graduate School|Tsinghua University Shenzhen International Graduate School]]、[[wiki/entities/organizations/Harbin Institute of Technology (Shenzhen)|Harbin Institute of Technology (Shenzhen)]]
- 产品/工具/基准：[[wiki/entities/products/Codex CLI|Codex CLI]]、[[wiki/entities/products/GPT-5.4-Mini|GPT-5.4-Mini]]、[[wiki/entities/products/SWE-bench Verified|SWE-bench Verified]]、[[wiki/entities/products/Live-SWE-Agent|Live-SWE-Agent]]、[[wiki/entities/products/Terminal Bench|Terminal Bench]]、[[wiki/entities/products/MHTBA|MHTBA]]、[[wiki/entities/products/OSWorld|OSWorld]]、[[wiki/entities/products/SeeAct|SeeAct]]、[[wiki/entities/products/Meta-Harness|Meta-Harness]]、[[wiki/entities/products/LinguaClaw|LinguaClaw]]

## 论断 / 证据

| 论断 | 证据 | 置信度 |
|---|---|---:|
| Harness policy 可以从 code harness 中外化为可执行自然语言文档。 | RQ1 中 NLAH+IHR 在 Live-SWE、MHTBA/TB2、OSWorld/SeeAct 上达到与 code/prompt realization 同量级的 task outcomes。 | 中高：来源实验支持，未独立复现 |
| NLAH 让 harness policy 更短、更可检查。 | 表 2 显示 Live-SWE policy materials 从 60.1k token 降至 2.9k，MHTBA 从 10.5k 降至 0.8k，OSWorld/SeeAct 从 47.5k 降至 1.4k。 | 高：来源审计支持 |
| IHR 能把自然语言 policy 物化为 contracts、tool use 与 recovery 行为。 | RQ2 中 NLAH 的 Artifact Contract、Tool Call Success、Failed Tool Continuation 指标较高。 | 中高：来源日志指标支持 |
| Handoff 是 IHR prototype 的主要弱点。 | RQ2 显示 NLAH 的 Orchestration Reliability 低于 Prompt，Information Handoff Recall 在 parent-child execution 下明显下降。 | 高：来源明确指出 |
| 显式 NLAH modules 可以被 ablate，从而分析哪些 harness 组件承重。 | RQ3 表 5 显示 file-backed state、self-evolution、evidence-backed answering 整体正向，而 multi-candidate search 和 context compression 有明显负面/混合结果。 | 高：来源实验支持 |
| 不能把“自然语言可执行 harness”理解为“自然语言替代所有代码”。 | 附录讨论明确分工：policy 用自然语言，exact mechanisms 仍应由 code/sandbox/validator 等承载。 | 高：来源明确声明 |

## 冲突 / 注意事项

- **Raw 元数据缺口：** raw frontmatter 的 `published` 为空；本页用 arXiv v2 submission date 记录，raw 未改。
- **HTML 渲染限制：** arXiv HTML 页面由 LaTeXML 生成，复杂表格/公式可能有渲染误差；关键数值已与 HTML/PDF 入口交叉读取，但本 wiki 未复现实验。
- **Prototype overhead：** IHR 当前实现有额外 model/tool calls 和 token 开销，不能只看最终 task score。
- **Prompt baseline 有时更强：** Live-SWE 与 MHTBA 中 prompt realization 得分高于 IHR-executed NLAH，因此 IHR 的价值不只是分数，而是可执行语义、可审计机制和模块化 ablation。
- **Handoff 风险：** parent-child execution 会损失信息，说明自然语言 harness 需要更强的 state/handoff 机制。
- **安全风险：** 论文指出外化可移植 harness logic 可能降低传播危险工作流的门槛；部署时需要 provenance tracking、review、permission control 和 sandbox isolation。

## 后续问题

- NLAH 与 `AGENTS.md` / skills 的边界在哪里：哪些规则应成为 vault/repo 级说明，哪些应成为可执行 harness module？
- IHR 的 handoff recall 低，是否说明 [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]] 需要更结构化的 state schema？
- NLAH 的可读 policy 能否与 Böckeler 的 feedforward/feedback model 合并，形成团队可维护的 user harness 模板？
- 如何对 NLAH 做安全审查，避免 prompt injection、malicious tool grafting 或 supply-chain contamination？
