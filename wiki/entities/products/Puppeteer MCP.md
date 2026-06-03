---
type: product
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Effective harnesses for long-running agents]]"
tags:
  - llm-wiki/entity/product
  - browser-automation
  - mcp
---
# Puppeteer MCP

## 在本 wiki 中的角色

Puppeteer MCP 是 Anthropic 来源中让 Claude 通过类用户交互测试 claude.ai clone 的浏览器自动化接口。

## 来源支持的要点

- 内嵌图片显示 Claude 通过 Puppeteer MCP 测试 claude.ai clone 时截取的截图。
- 文章称浏览器自动化工具帮助 Claude 发现并修复仅靠读代码不明显的 bug。
- 来源也指出限制：Claude 无法通过 Puppeteer MCP 看到浏览器原生 alert modal，因此依赖这些 modal 的功能更容易出问题。

## 相关概念

- [[wiki/concepts/Self-verification|Self-verification]]
- [[wiki/concepts/Harness Engineering|Harness Engineering]]
- [[wiki/entities/products/Chrome DevTools MCP|Chrome DevTools MCP]]
