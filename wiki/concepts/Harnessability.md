---
type: concept
status: draft
created: 2026-05-29
updated: 2026-05-29
sources:
  - "[[wiki/sources/2026-05-28 Harness engineering for coding agent users]]"
tags:
  - llm-wiki/concept
  - harness-engineering
  - architecture
---
# Harnessability

## 定义

可工作支架化程度（Harnessability）是一个代码库、架构或技术栈被 agent harness 有效调节的难易程度。它取决于哪些规则、信号、边界和工具能被清晰表达并接入 agent 工作流。

## 为什么重要

不是所有代码库都同样适合高自治 coding agent。强类型、清晰模块边界、成熟框架和可执行约束会天然提供 sensors/guides；技术债务重、边界模糊、工具缺失的 legacy 系统往往最需要 harness，却最难 harness。

## 来源支持的要点

- Böckeler 指出，强类型语言天然提供 type checking sensor。
- 清晰模块边界让架构约束规则可定义。
- Spring 等框架抽象掉细节，降低 agent 需要处理的复杂度，从而隐式提高成功概率。
- Greenfield 团队可以从第一天把 harnessability 烘焙进技术和架构选择。
- Legacy 团队面对更难的问题：harness 最需要的地方，通常也是最难搭建的地方。

## 相关概念

- [[wiki/concepts/Harness Templates|Harness Templates]]
- [[wiki/concepts/Mechanized Invariants|Mechanized Invariants]]
- [[wiki/concepts/Agent-readable Codebase|Agent-readable Codebase]]
- [[wiki/concepts/Coding Agent User Harness|Coding Agent User Harness]]

## 开放问题

- 如何评估一个代码库的 harnessability？
- Harnessability 是否会成为技术选型的一等指标？
- 如何逐步提高 legacy 系统的 harnessability，而不先进行大型重构？
