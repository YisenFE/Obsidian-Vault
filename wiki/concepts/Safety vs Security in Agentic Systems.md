---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
tags:
  - llm-wiki/concept
  - safety
  - security
  - agentic-systems
---
# Safety vs Security in Agentic Systems

## 定义

Agentic systems 中的安全性可以拆成两层：安全/安全策略（Security）偏向权限、隔离和资源访问边界；安全行为/安全对齐（Safety）偏向模型是否应该提出某个 tool call 或行动。Bolin 在 Codex 访谈中强调这两个词常被混用，但含义不同。

## 为什么重要

如果把二者混在一起，就容易误以为 sandbox 能解决所有风险，或误以为模型 safety 能替代本地权限控制。Coding agent 同时需要：模型尽量不提出危险动作，以及 harness 即使收到危险/错误命令也能按权限边界执行。

## 来源支持的要点

- Bolin 将 security 描述为：工具能否读写哪些 folder、在什么 policy 下运行。
- 他将 safety 更多放在 back-end/model side：确保模型提出的 tool calls 本身安全或合适。
- 如果 fork Codex 但仍使用 OpenAI models，就依赖 OpenAI 模型侧 safety；如果换成其他模型，则 safety 状态更不确定。
- Harness 在某种意义上是 faithfully executing tool calls，因此需要 sandbox 作为 backstop。

## 相关概念

- [[wiki/concepts/Sandbox and Tool Orchestration|Sandbox and Tool Orchestration]]
- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Agent Loop|Agent Loop]]

## 开放问题

- 哪些风险必须由 model safety 处理，哪些必须由 local sandbox/security policy 处理？
- 当用户替换模型或 fork agent runtime 时，安全责任如何重新划分？
- 如何测试 coding agent 的 security boundary 与 safety behavior？
