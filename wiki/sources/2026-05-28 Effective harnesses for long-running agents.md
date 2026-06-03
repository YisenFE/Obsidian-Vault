---
type: source-summary
status: ingested
created: 2026-05-29
updated: 2026-05-29
source: "[[raw/2026-05-28 Effective harnesses for long-running agents]]"
external_url: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
author: Justin Young
published: 2025-11-26
image_assets:
  - "[[raw/assets/2026-05-28-anthropic-long-running-agents-puppeteer.gif]]"
tags:
  - llm-wiki/source
  - anthropic
  - harness-engineering
  - long-running-agents
---
# Effective harnesses for long-running agents

## 一句话结论

Anthropic 把长时程 agent 的核心问题定义为“跨 context/session 的交接失败”，并提出 initializer agent + coding agent、结构化 feature list、progress file、git history、`init.sh` 和端到端浏览器验证这一组 harness 机制。

## 来源元数据

- 原始资料： [[raw/2026-05-28 Effective harnesses for long-running agents]]
- 外部链接： [Anthropic — Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)
- 作者： [[wiki/entities/people/Justin Young|Justin Young]]
- 发表时间： 2025-11-26（官方页面显示；raw frontmatter 未记录）
- 本地图片资产（ingest 时已读取）：
  - ![[raw/assets/2026-05-28-anthropic-long-running-agents-puppeteer.gif]]

## 关键要点

1. 长时程 agent 的核心限制不是单次上下文压缩本身，而是复杂任务必须跨多个离散 session；每个新 session 默认没有上一轮工作记忆。
2. 仅靠 compaction 不足以支撑生产级应用开发：Anthropic 观察到 Claude 可能一次性做太多，导致半成品无人记录；也可能在后期看到已有进展后过早宣布完成。
3. Anthropic 的两段式方案是：第一次运行使用 **initializer agent** 建立环境和任务边界；后续运行使用 **coding agent** 每次只做增量进展，并留下结构化交接物。
4. Initializer 负责创建 `init.sh`、`claude-progress.txt`、初始 git commit，以及一个覆盖完整目标的 feature list；feature list 中的功能先全部标为 failing。
5. Coding agent 每轮开始时读取 progress file、git log、feature list 和 `init.sh`，先运行基础端到端测试确认系统没有被上轮破坏，再选择一个未完成高优先级 feature。
6. Feature list 使用 JSON，并要求 coding agent 只改 `passes` 状态，不得删除或改写测试描述；这是为了避免 agent 通过修改验收标准来“完成”任务。
7. 每轮结束时，agent 应保持代码在可合并的 clean state：无重大 bug、结构有序、有必要文档，并写入 git commit 与 progress 更新。
8. 文章强调端到端验证：在 web app 场景中，Claude 需要像人类用户一样通过浏览器自动化测试功能，而不仅是运行单元测试或 `curl`。
9. 该方案仍有边界：Claude 的视觉与浏览器自动化工具不能捕获所有 bug；例子中 Puppeteer MCP 无法看到浏览器原生 alert modal，因此相关功能更容易出问题。
10. 未来问题包括：单一通用 coding agent 是否优于多 agent 架构，以及这些模式如何迁移到科学研究、金融建模等非 web app 长任务。

## 需要更新的概念

- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]]
- [[wiki/concepts/Feature List as Test Contract|Feature List as Test Contract]]
- [[wiki/concepts/Self-verification|Self-verification]]
- [[wiki/concepts/Agent-readable Codebase|Agent-readable Codebase]]
- [[wiki/concepts/Repository as System of Record|Repository as System of Record]]
- [[wiki/concepts/Mechanized Invariants|Mechanized Invariants]]

## 需要更新的实体

- 人物： [[wiki/entities/people/Justin Young|Justin Young]]
- 组织： [[wiki/entities/organizations/Anthropic|Anthropic]]
- 产品/工具： [[wiki/entities/products/Claude Agent SDK|Claude Agent SDK]], [[wiki/entities/products/Claude Code|Claude Code]], [[wiki/entities/products/Puppeteer MCP|Puppeteer MCP]]

## 论断 / 证据

| 论断 | 证据 | 置信度 |
|---|---|---:|
| 长时程 agent 需要显式跨会话交接工件，而不只是上下文压缩。 | 文章称每个新 session 默认没有记忆，compaction 也不能可靠传递清晰指令；方案核心是 progress file 与 git history。 | 高：来源支持 |
| 专门的首次 initializer prompt 有助于避免一次性做太多和过早宣布完成。 | Initializer 在 coding agent 开始增量工作前创建 feature requirements、`init.sh`、progress notes 和初始 commit。 | 高 |
| Feature list 应被视为测试契约，而不是可随意编辑的计划笔记。 | Anthropic 使用 JSON，并要求 agent 只改 `passes`，不能编辑/删除测试，以避免功能缺失或有 bug。 | 高 |
| 浏览器级端到端测试能明显改善 Web app agent 的表现。 | 来源称明确要求 Claude 使用浏览器自动化、像人类用户一样测试后，更容易发现和修复 bug。 | 中高：来源自述 |
| 该 harness 未必能原样迁移到 full-stack web app 之外。 | 文章称 demo 针对 Web app 开发优化，并把其他领域列为未来工作。 | 高 |

## 冲突 / 注意事项

- **Raw 元数据缺口：** raw frontmatter 中 `author` 与 `published` 为空；本页作者来自正文，发布日期来自官方页面。
- **来源自述：** 性能改善和失败模式来自 Anthropic 自己的实验；本次 ingest 未独立复现。
- **工具限制：** Puppeteer/浏览器自动化和模型视觉仍会漏掉某些 UI 状态，尤其是示例中的浏览器原生 alert modal。
- **领域特异性：** 示例集中在 full-stack Web app；能否迁移到研究、金融或其他长时程任务仍是开放问题。

## 后续问题

- Anthropic 的 initializer/coding-agent 模式与 OpenAI 的 repository-as-system-of-record、mechanized invariants 有何关系？
- 长时程 agent harness 应该标准化使用 JSON feature list，还是某些 Obsidian/Dataview/task file 更合适？
- 跨会话交接工件和真正长期记忆的边界在哪里？
