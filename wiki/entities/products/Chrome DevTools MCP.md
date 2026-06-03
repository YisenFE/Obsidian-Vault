---
type: product
status: draft
created: 2026-05-28
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 工程技术：在智能体优先的世界中利用 Codex]]"
tags:
  - llm-wiki/entity/product
  - browser-automation
  - mcp
---
# Chrome DevTools MCP

## 在本 wiki 中的角色

Chrome DevTools MCP 是 OpenAI 来源中的浏览器/运行时接口，用来让 [[wiki/entities/products/Codex|Codex]] 在验证阶段检查并驱动应用。

## 来源支持的要点

- 来源称 Chrome DevTools protocol 被连接到 agent runtime。
- DOM 快照、截图和导航 skills 让 Codex 能复现错误、验证修复并推理 UI 行为。
- 图示显示 Codex 选择目标、清理 console 状态、截取前后快照、触发 UI 路径、观察运行时事件、应用修复、重启并重新验证直到干净。

## 相关概念

- [[wiki/concepts/Agent-readable Codebase|Agent-readable Codebase]]
- [[wiki/concepts/Harness Engineering|Harness Engineering]]
