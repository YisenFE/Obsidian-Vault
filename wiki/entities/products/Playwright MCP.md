---
type: product
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Harness design for long-running application development]]"
tags:
  - llm-wiki/entity/product
  - browser-automation
  - mcp
---
# Playwright MCP

## 在本 wiki 中的角色

Playwright MCP 是 Anthropic evaluator agents 用来像用户一样操作 live frontend/full-stack applications 的浏览器自动化接口。

## 来源支持的要点

- 在 frontend design loop 中，evaluator 使用 Playwright MCP 导航页面、截图并检查实时实现，再根据 criteria 评分。
- 在 full-stack harness 中，evaluator 像用户一样点击运行中的 app，并测试 UI 行为、API endpoints 和数据库状态。
- Playwright MCP 让外部评估超越静态截图，但每轮主动导航/评估都会增加真实 wall-clock 时间。

## 相关概念

- [[wiki/concepts/External Evaluator Agent|External Evaluator Agent]]
- [[wiki/concepts/Self-verification|Self-verification]]
- [[wiki/entities/products/Puppeteer MCP|Puppeteer MCP]]
- [[wiki/entities/products/Chrome DevTools MCP|Chrome DevTools MCP]]
