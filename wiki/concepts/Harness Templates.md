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
  - templates
---
# Harness Templates

## 定义

工作支架模板（Harness Templates）是针对常见服务拓扑预先打包的结构、技术栈、guides 和 sensors，让团队在实例化一个服务或应用时，同时获得适配该拓扑的 coding-agent harness。

## 为什么重要

许多企业有覆盖大部分需求的少数服务拓扑，例如数据看板、CRUD business service、event processor。若这些拓扑已有 service template，下一步可能是附带 agent harness template，使 agent 从一开始就被牵引到正确结构、约定和检查体系中。

## 来源支持的要点

- Böckeler 预测 service templates 可能演化为 harness templates。
- 图示例子包括 Data dashboard in Node、CRUD Business Service on JVM、Event processor in Golang。
- Harness template 由 topology 的 structure definition、tech stack、guides 和 sensors 组成。
- 团队未来可能部分基于已有 harness 来选择技术栈和结构。
- 文章也指出模板实例化后会与上游改进脱节；包含非确定性 guides/sensors 的 harness templates 可能比传统 service templates 更难测试、版本化和贡献。

## 相关概念

- [[wiki/concepts/Harnessability|Harnessability]]
- [[wiki/concepts/Coding Agent User Harness|Coding Agent User Harness]]
- [[wiki/concepts/Feedforward Guides|Feedforward Guides]]
- [[wiki/concepts/Feedback Sensors|Feedback Sensors]]

## 开放问题

- Harness template 应如何版本化，并同步到已实例化服务？
- 如何测试一个模板中的 inferential guide 或 review agent 没有退化？
- 模板应由平台团队、架构团队还是业务团队维护？
