---
type: concept
status: draft
created: 2026-06-01
updated: 2026-06-01
aliases:
  - Evidence-backed research audit
  - Research Goal
sources:
  - "[[wiki/sources/2026-06-01 Using Goals in Codex]]"
  - "[[wiki/sources/2026-05-28 Natural-Language Agent Harnesses]]"
tags:
  - llm-wiki/concept
  - research
  - goals
  - evidence
---
# Research Goal Audit

## 定义

Research Goal Audit（研究目标审计）是把研究/复现任务写成 Goal：先列出主张，再映射证据，尝试可行复现，明确 approximate reconstruction、blocked exact replay 和 remaining uncertainty，最后交付 claim-by-claim ledger。

## 为什么重要

研究型 agent 很容易把“生成了一份像样报告”误当成“完成研究”。Research Goal Audit 要求 agent 保存不同证据等级，避免把近似结果、代理支持和原始实验 replay 混为一谈。

## 来源支持的要点

- Deep Hedging case study 中，强 Goal 要求 attempted headline results、verify outputs，并区分 reproduced mechanics、approximate trained results、blocked exact replay、remaining uncertainty。
- Codex 重建了 pricing/hedging mechanics、Heston reference price、CVaR hedge policies、histogram/hedge-surface artifacts、transaction-cost slope 等部分。
- 精确 replay 被 blocker 限制：缺少 random seeds、generated training paths、TensorFlow graph、optimizer state、checkpoints、full original simulation state。
- 最终报告应保留 support levels：close approximate reproduction 不等于 exact replay。
- NLAH 的 evidence-backed answering 和 claim/evidence separation 与该模式一致。

## 相关概念

- [[wiki/concepts/Goal Completion Contract|Goal Completion Contract]]
- [[wiki/concepts/Evidence-Based Completion|Evidence-Based Completion]]
- [[wiki/concepts/Artifact Contract|Artifact Contract]]
- [[wiki/concepts/Natural-Language Agent Harnesses|Natural-Language Agent Harnesses]]

## 开放问题

- 研究审计的 status taxonomy 应如何标准化？
- 近似 reproduction 与 exact replay 的边界如何定量？
- 何时应停止继续训练/调参，转而报告 blocker？
