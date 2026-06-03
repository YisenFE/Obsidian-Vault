---
type: product
status: stub
created: 2026-06-03
updated: 2026-06-03
sources:
  - "[[wiki/sources/2026-06-03 A harness for every task dynamic workflows in Claude Code]]"
tags:
  - llm-wiki/entity/product
  - developer-tooling
---
# Bun

## 在本 wiki 中的角色

Bun 是 Claude Code dynamic workflows 来源中的迁移/重构用例：文章称 Bun 从 Zig 到 Rust 的重写使用了 workflows，并引用 Jarred 的 X thread。

## 来源支持的要点

- 该来源把 Bun 案例用作大规模 migration/refactor 的例子：按 callsite、失败测试、模块等拆分，再让子智能体在 worktree 中修复、review 和合并。
- 该案例来自文章引用的外部 X thread；本 wiki 当前未独立核验迁移细节。

## 相关概念

- [[wiki/concepts/Dynamic Workflows|Dynamic Workflows]]
- [[wiki/concepts/Parallel Agent Workflows|Parallel Agent Workflows]]
