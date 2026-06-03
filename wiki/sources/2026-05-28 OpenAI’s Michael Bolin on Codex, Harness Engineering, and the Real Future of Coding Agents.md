---
type: source-summary
status: ingested
created: 2026-05-29
updated: 2026-05-29
source: "[[raw/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
external_url: https://www.youtube.com/watch?v=6BAqgT3qe98
author: "[[wiki/entities/people/Ksenia|Ksenia]]"
published: 2026-03-14
tags:
  - llm-wiki/source
  - codex
  - harness-engineering
  - coding-agents
  - interview
---
# OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents

## 一句话结论

这篇访谈把 [[wiki/entities/products/Codex|Codex]] 的 harness 描述为“agent loop + sandbox + tool orchestration”的工程层：模型最终决定体验上限，但要让 coding agent 在真实开发者机器上可靠、安全地工作，仍需要小而紧的 harness、强沙箱、少量强工具、良好的仓库/文档结构，以及让 agent 自己探索代码库的空间。

## 来源元数据

- 原始资料：[[raw/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]
- 外部链接：[YouTube — OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents](https://www.youtube.com/watch?v=6BAqgT3qe98)
- Transcript 链接：[Turing Post — bolincodex](https://www.turingpost.com/p/bolincodex)
- 访谈者：[[wiki/entities/people/Ksenia|Ksenia]] / [[wiki/entities/organizations/Turing Post|Turing Post]]
- 嘉宾：[[wiki/entities/people/Michael Bolin|Michael Bolin]]，来源称其为 OpenAI Codex open-source tech lead。
- 发表时间：2026-03-14（raw frontmatter 已记录）

## 关键要点

1. Michael Bolin 的立场不是“模型或 harness 二选一”：模型会主导最终体验，但 harness 仍有大量创新空间；OpenAI Codex 团队的关键在于工程侧与研究侧共同开发 agent。
2. 他把 harness 定义为 [[wiki/concepts/Agent Loop|agent loop]]：给模型上下文和可用工具，模型返回下一步，通常是 tool call；harness 执行工具并把结果返回给模型。
3. Codex 的 harness 特别重视 [[wiki/concepts/Sandbox and Tool Orchestration|sandboxing 与 tool orchestration]]，因为 coding agent 会在用户机器上运行 shell/computer-use 命令。
4. Codex 针对不同 OS 使用不同 sandbox 机制：macOS 用 Seatbelt，Linux 用 Bubble Wrap、seccomp、Landlock，Windows 使用自研 sandbox；访谈称部分实现可在 open-source repo 中看到。
5. Bolin 明确区分 security 与 safety：security 更像权限/文件系统/工具执行边界；safety 更多发生在后端模型侧，即模型先判断哪些 tool calls 适合提出。
6. Codex app 被描述为 mission control interface：开发者可以管理多条 agent conversation、浏览 diff，并随时打开 terminal；这对应从单 IDE 工作转向多 agent 并行 workstreams。
7. Coding agent 改变开发者日常的第一件事是 throughput：Bolin 自述会使用多个 Codex repo clone，在会议间隙给不同任务发消息，让多个 workstreams 持续推进。
8. 新的 developer inner loop 不只是写代码，而是优化 agent workflow：是否把重复做法变成 skill、是否共享给队友、如何让 Codex 做 code review。
9. Agent-first world 让旧的工程最佳实践重新变得“明显值得”：文档、测试驱动开发、清晰命名、严格架构、可执行测试说明和 modest `AGENTS.md` 都更重要。
10. Codex 团队倾向把 `AGENTS.md` 做得 modest：只记录 agent 不容易从代码快速发现的信息，例如测试怎么跑、哪些测试更重要；不要写成与源码并行且可能腐化的长文档。
11. 对 context engineering，Bolin 倾向给 agent 一段任务描述、必要文件指针和可用工具/PR/GitHub context，但不强行规定解决路径；让 Codex 自己 grep/read code 并形成判断。
12. Codex 的 design bias 是 [[wiki/concepts/Small Powerful Tool Surface|少量强工具]]：例如不提供显式 read-file tool，而是给 terminal control，让模型用 `cat`、`sed` 等系统工具读文件。
13. 当工具输出可能很大时，访谈建议让 Codex 把结果写到文件，再按需读取，而不是把巨量输出直接塞进上下文窗口。
14. Bolin 认为对 coding tasks 来说，sandboxing 在很多场景中可以替代频繁 human-in-the-loop；如果用户同时跑多个 agent，每几分钟手动介入会限制吞吐。
15. Harness 仍需高 reliability、performance 与资源节制：如果 harness 自身崩溃，session 就结束；harness 应尽量做 bare minimum，把资源留给模型实际解决问题。
16. 未来方向包括 multi-agent/sub-agent、跨机器 agent network、terminal tool、memory、context connectors、browser/email/doc actions，以及更强的 context window 与 compaction。

## 术语说明

- Agent Loop（智能体循环）：harness 调用模型、执行模型提出的 tool call、把结果返回模型的循环。
- Sandboxing（沙箱隔离）：限制 agent 命令能读写/访问哪些资源的执行边界。
- Tool Orchestration（工具编排）：harness 安排模型如何调用 terminal、web、computer-use 等工具，并在不同 OS/security policy 下执行。
- Small Powerful Tool Surface（少量强工具界面）：减少专门工具数量，给 agent 更通用、更强的操作原语，例如 terminal。
- Context Engineering（上下文工程）：为 agent 提供任务描述、文件指针、PR/GitHub context、文档和工具入口，同时避免过量/陈旧上下文。

## 需要更新的概念

- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Agent Loop|Agent Loop]]
- [[wiki/concepts/Sandbox and Tool Orchestration|Sandbox and Tool Orchestration]]
- [[wiki/concepts/Safety vs Security in Agentic Systems|Safety vs Security in Agentic Systems]]
- [[wiki/concepts/Small Powerful Tool Surface|Small Powerful Tool Surface]]
- [[wiki/concepts/Context Engineering for Coding Agents|Context Engineering for Coding Agents]]
- [[wiki/concepts/Agent-readable Codebase|Agent-readable Codebase]]
- [[wiki/concepts/Coding Agent User Harness|Coding Agent User Harness]]
- [[wiki/concepts/Agent Memory and Session Handoff|Agent Memory and Session Handoff]]
- [[wiki/concepts/Context Reset vs Compaction|Context Reset vs Compaction]]

## 需要更新的实体

- 人物：[[wiki/entities/people/Michael Bolin|Michael Bolin]]、[[wiki/entities/people/Ksenia|Ksenia]]
- 组织：[[wiki/entities/organizations/OpenAI|OpenAI]]、[[wiki/entities/organizations/Turing Post|Turing Post]]
- 产品/工具：[[wiki/entities/products/Codex|Codex]]、[[wiki/entities/products/Codex CLI|Codex CLI]]、[[wiki/entities/products/Codex App|Codex App]]、[[wiki/entities/products/GPT-5|GPT-5]]、[[wiki/entities/products/VS Code|VS Code]]、[[wiki/entities/products/JetBrains|JetBrains]]、[[wiki/entities/products/Xcode|Xcode]]

## 论断 / 证据

| 论断 | 证据 | 置信度 |
|---|---|---:|
| Codex harness 的核心是 agent loop、工具执行和 sandbox policy。 | Bolin 在 1:20 起把 harness 定义为调用模型、执行 tool call、返回结果的 loop，并在 2:08 起强调 Codex harness 会把 shell/computer-use commands 放进 sandbox 或用户指定 policy。 | 高：访谈直接陈述 |
| Security 与 safety 在 agentic system 中应区分。 | Bolin 说 security 更像“工具能否读写哪些 folder”，safety 更多是后端模型决定哪些 tool calls 适合提出。 | 高：访谈直接陈述 |
| Codex 倾向小而紧的 harness 和少量强工具。 | Bolin 说 Codex 会尽量让 harness small/tight，给少量 very powerful tools；例如不提供显式读文件工具，而是给 terminal。 | 高：访谈直接陈述 |
| Agent-first workflow 提升吞吐，但要求开发者管理多个 workstreams。 | Bolin 自述会同时维护多个 Codex repo clone，并在会议间隙推动多个任务。 | 中高：个人实践陈述 |
| 文档、TDD、架构和 `AGENTS.md` 在 agent-first world 中更有价值。 | Bolin 认为这些长期 best practices 因 agent 需要导航代码库而变得明显值得，并强调 modest `AGENTS.md` 记录 agent 不易从代码发现的信息。 | 中高：访谈判断 |
| 过量 context 可能不如让 agent 自己探索。 | Bolin 倾向给任务段落、必要文件指针和可用工具，不强行规定路径；大输出写文件而不是塞入 context。 | 中：经验性判断 |

## 冲突 / 注意事项

- **来源类型：** 这是访谈/YouTube transcript，不是 benchmark 或论文；论断多是 Michael Bolin 的经验判断和产品团队视角。
- **姓名转写：** transcript 开头把嘉宾转写为 “Michael Boland”，但标题、guest 信息和链接均指向 Michael Bolin；本 wiki 以 Michael Bolin 为准，raw 未改。
- **增长数据自述：** “5x usage”、CLI/VS Code/app 时间线、Codex app adoption 等均来自访谈自述，未独立验证。
- **产品状态可能变化：** Codex app、VS Code/JetBrains/Xcode integration、sandbox implementation 都是来源时间点陈述。
- **安全边界需实测：** 访谈解释了设计原则，但本 wiki 未审计 Codex repo sandbox 代码或实际权限边界。

## 后续问题

- Codex 的 small-tool-surface 思路与 NLAH/IHR 的可执行 policy runtime 是否存在张力？
- 什么时候 terminal 这类强通用工具优于 read-file、edit-file、search 等专用工具？
- “Sandboxing 替代 frequent human-in-the-loop”在哪些 coding task 上成立，在哪些高风险任务上不成立？
- `AGENTS.md` 应如何保持 modest，同时又能提供足够 context 给 agent？
