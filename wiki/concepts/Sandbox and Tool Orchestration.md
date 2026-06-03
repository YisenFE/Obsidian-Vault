---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
  - "[[wiki/sources/2026-05-28 The Anatomy of an Agent Harness]]"
  - "[[wiki/sources/2026-06-01 The Shorthand Guide to Everything Claude Code]]"
tags:
  - llm-wiki/concept
  - sandbox
  - tool-orchestration
  - security
---
# Sandbox and Tool Orchestration

## 定义

沙箱与工具编排（Sandbox and Tool Orchestration）是 harness 负责把模型提出的 tool calls 放进受控执行环境，并根据平台、权限和用户策略决定工具如何运行、能访问哪些资源、结果如何返回 agent loop 的机制。

## 为什么重要

Coding agent 会执行 shell、terminal、browser 或 computer-use 动作；这些动作直接影响用户机器和代码库。Sandbox 是让 agent 能自主探索同时不“run wild”的关键 backstop，tool orchestration 则决定强工具如何安全、可靠、低开销地进入 loop。

## 来源支持的要点

- Bolin 说 Codex harness 会把 shell/computer-use commands 放入 sandbox，或按用户给 agent 的 policy 执行。
- Codex 按 OS 使用不同机制：macOS Seatbelt，Linux Bubble Wrap、seccomp、Landlock，Windows 自研 sandbox。
- Bolin 把 sandboxing 视为 coding tasks 中替代频繁 human-in-the-loop 的主要机制之一。
- NLAH 论文也强调自然语言 policy 之外，tool execution、sandboxing、benchmark adapters、logging 和 validators 仍应由代码机制承载。

- LangChain Anatomy 来源把 sandbox 视为让 agent 安全运行代码、检查文件、安装依赖和完成任务的 operating environment。
- Sandboxes 也解决规模问题：环境可按需创建、并行 fan-out、多任务完成后销毁。
- 文章强调 default tooling 也是 harness 责任：预装语言运行时、包、git/testing CLI、browser、logs、screenshots 和 test runners，使 agent 能观察与验证。

- Claude Code shorthand 来源提醒 risky operations 使用 sandbox mode，并警告 `--dangerously-skip-permissions` 会让 Claude 大范围行动，可能造成破坏。
- Subagent allowed tools/MCPs/permissions 是用户侧 tool orchestration 的另一层边界。

## 相关概念

- [[wiki/concepts/Safety vs Security in Agentic Systems|Safety vs Security in Agentic Systems]]
- [[wiki/concepts/Agent Loop|Agent Loop]]
- [[wiki/concepts/Small Powerful Tool Surface|Small Powerful Tool Surface]]
- [[wiki/concepts/Harness Policy Layer|Harness Policy Layer]]

- [[wiki/concepts/Subagent Scoping|Subagent Scoping]]

## 开放问题

- Sandbox policy 应默认保守，还是允许用户按任务放宽？
- 不同 OS 的 sandbox 能力差异会不会影响 agent behavior 和 benchmark 可比性？
- 如何把 sandbox policy 暴露给 agent，使其能规划但不能绕过？
