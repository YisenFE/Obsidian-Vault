---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
  - "[[wiki/sources/2026-06-01 Using Goals in Codex]]"
tags:
  - llm-wiki/concept
  - harness-engineering
  - agent-loop
---
# Agent Loop

## 定义

智能体循环（Agent Loop）是 harness 调用模型、给出任务上下文和可用工具、接收模型下一步 action/tool call、执行该 action 并把结果返回模型的循环。它是 coding agent 从一次静态回答变成多步执行系统的基础。

## 为什么重要

Agent loop 决定模型能看到什么、能调用什么工具、工具结果如何回到上下文、失败如何恢复、何时停止。模型能力再强，如果 loop 的工具、权限、反馈或可靠性设计不好，也无法稳定工作。

## 来源支持的要点

- Bolin 在 Codex 访谈中把 harness / agent loop 描述为：给模型上下文、任务和工具列表，模型返回下一步，通常是 tool call；harness 执行工具并把结果反馈给模型。
- 工具可以很简单，如执行命令并返回 stdout/exit code；也可以更交互，如控制 terminal session、computer-use 或 web search。
- NLAH 论文则把相似 loop 抽象为 IHR 执行 NLAH policy：agent calls、handoffs、state updates、validation gates 和 artifact contracts。
- Agent loop 的 reliability 是承重组件：Bolin 说如果 harness falls over，session 就结束。

- LangChain Anatomy 来源把常见 agent execution pattern 描述为 [ReAct loop](https://docs.langchain.com/oss/python/langchain/agents)：模型 reasoning、通过工具 action、观察结果并重复。
- 同文也指出最简单的聊天产品本身就是 while-loop harness：保存历史消息、追加新用户消息，再调用模型。
- Agent loop 与 bash/code execution 组合后，模型可以通过工具调用在环境中写代码、运行代码、观察结果，再继续规划。

- Codex Goals 来源把普通 prompt loop 与 Goal loop 区分开：prompt 是 ask → work → result → wait；Goal 是 work → check → next step/complete，并跨 turn 保持目标。
- Goal continuation 仍然受 dispatcher gate 控制，只有 thread idle、Goal active、无 queued user input 且 within budget 时才继续。

## 相关概念

- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/concepts/Sandbox and Tool Orchestration|Sandbox and Tool Orchestration]]
- [[wiki/concepts/Middleware Hooks|Middleware Hooks]]
- [[wiki/concepts/Intelligent Harness Runtime|Intelligent Harness Runtime]]

- [[wiki/concepts/Bash and Code Execution|Bash and Code Execution]]
- [[wiki/concepts/Ralph Loop|Ralph Loop]]

- [[wiki/concepts/Goal Lifecycle and Continuation Gates|Goal Lifecycle and Continuation Gates]]

## 开放问题

- Agent loop 应该由少量通用工具驱动，还是为常见动作提供更多专用工具？
- Loop 的停止条件应由模型决定、由 harness gate 决定，还是二者结合？
- 如何评估 agent loop 的 reliability、latency 和 resource efficiency？
