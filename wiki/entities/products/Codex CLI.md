---
type: product
status: stub
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
  - "[[wiki/sources/2026-05-28 OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents]]"
  - "[[wiki/sources/2026-06-01 Using Goals in Codex]]"
tags:
  - llm-wiki/entity/product
  - natural-language-harness
---
# Codex CLI

## 在本 wiki 中的角色

NLAH 论文实验使用的 agent runtime/CLI；来源记录版本为 0.123.0。

## 来源支持的要点

- 论文所有实验使用 Codex CLI 0.123.0、`gpt-5.4-mini` 和 reasoning effort `xhigh`。

- Michael Bolin 访谈把 Codex CLI 放在开发者不同入口之一：terminal 用户使用 CLI，IDE 用户使用 VS Code / JetBrains / Xcode integration，Codex App 则是新的 mission-control surface。

- Using Goals in Codex 来源给出 Codex Goals 的命令表面：`/goal <outcome>`、`/goal`、`/goal pause`、`/goal resume`、`/goal clear`；并称 Goals 从 Codex 0.128.0 开始可用。

## 相关页面

- [[wiki/sources/2026-05-28 Natural-Language Agent Harnesses|Natural-Language Agent Harnesses]]
- [[wiki/concepts/Natural-Language Agent Harnesses|Natural-Language Agent Harnesses]]
