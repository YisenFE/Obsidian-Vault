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
  - regulation
---
# Harness Regulation Categories

## 定义

工作支架调节类别（Harness Regulation Categories）是按 harness 试图调节的目标状态对控制进行分类。Böckeler 暂分为 maintainability harness、architecture fitness harness 和 behaviour harness。

## 为什么重要

“Harness” 过于宽泛。按调节目标分类后，可以更清楚地讨论哪些控制可行、哪些风险仍需人工监督，以及某个 harness 到底在保护内部质量、架构特性，还是功能行为。

## 来源支持的要点

- Maintainability harness 调节内部代码质量和可维护性，是当前最容易 harness 的类别，因为已有大量测试、lint、coverage、复杂度和结构分析工具。
- Architecture fitness harness 调节架构特性，例如性能要求、观测性约定、日志标准、模块边界和 fitness functions。
- [[wiki/concepts/Behaviour Harness|Behaviour Harness]] 调节功能行为，是最难的问题，因为 AI 生成测试、coverage 和人工测试的组合还不足以大幅降低监督。
- 图示把 guides/sensors 作为横轴，把 maintainability、architecture fitness、behaviour 作为纵向调节维度。

## 相关概念

- [[wiki/concepts/Behaviour Harness|Behaviour Harness]]
- [[wiki/concepts/Mechanized Invariants|Mechanized Invariants]]
- [[wiki/concepts/Feedback Sensors|Feedback Sensors]]
- [[wiki/concepts/Harness Engineering|Harness Engineering]]

## 开放问题

- Security、reliability、product quality 是否应成为单独类别，还是归入 architecture/behaviour？
- 一个 control 同时影响多个类别时如何建模？
- 如何评价每个 regulation category 的覆盖率？
