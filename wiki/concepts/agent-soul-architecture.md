---
title: Agent SOUL 架构
created: 2026-05-08
updated: 2026-05-08
type: concept
tags: [agent, ai-tool, best-practice]
sources: [conversation/2026-05-07]
related: [soul-md, mercury-agent, hermes-agent]
---

# Agent SOUL 架构概念

从 [[soul-md]] 和 [[mercury-agent]] 两个案例中抽象出的共同架构概念。

## 核心思想

AI Agent 的人格和行为规范通过**用户可编辑的 markdown 文件**定义，而非硬编码在系统提示中。

这一范式的关键特征：

1. **用户主权**：用户拥有和编辑 Agent 的"灵魂"文件，而非依赖平台预设
2. **透明可审计**：Agent 的行为准则以人类可读的 markdown 呈现
3. **版本可控**：可以用 git 追踪 Agent 人格的演变历史
4. **双向约束**：不仅约束 Agent 行为，也约束用户（如发布需批准）

## 两种实现路径

### 路径一：Hermes 的 SOUL.md（单文件、大而全）

- **来源**：Tony Simons 的 170 行 SOUL.md 框架 → 详见 [[soul-md]]
- **特点**：一个文件包含所有内容（身份、性格、反对义务、约束、项目地图、输出标准、问责循环）
- **优势**：简单直观、一个文件搞定、迁移方便
- **劣势**：文件膨胀后难以维护、不同关注点耦合

### 路径二：Mercury 的多文件分离

- **来源**：cosmicstack-labs/mercury-agent → 详见 [[mercury-agent]]
- **特点**：拆分为 `soul.md` + `persona.md` + `taste.md` + `heartbeat.md`
- **优势**：关注点分离、每个文件可独立演进、便于模块化复用
- **劣势**：多文件管理复杂度增加、需要跨文件一致性保障

### 设计权衡

| 维度 | 单文件（SOUL.md） | 多文件分离（Mercury） |
|------|------------------|---------------------|
| 上手难度 | 低 | 中 |
| 可维护性 | 短期好，长期差 | 持续良好 |
| 便携性 | 极高（一个文件） | 中（需打包多文件） |
| 适合场景 | 个人/小项目 | 团队/多 Agent |

## 相关概念

- **Agent Memory Systems**：[[mempalace]]（宫殿式记忆）、[[hindsight-memory]]（知识图谱记忆）、Mercury 的 SQLite+FTS5 结构化记忆
- **Prompt Engineering**：SOUL 文件本质上是一种高级 prompt engineering，将 system prompt 从代码中解耦到用户可编辑的文件
- **User-Agent Alignment**：通过用户定义的"灵魂"文件确保 Agent 行为与用户意图对齐，而非依赖 AI 公司的通用对齐策略

## 未来方向

- SOUL 文件的标准化和互操作性（不同 Agent 平台间共享人格定义）
- 从静态 markdown 演进为可编程的 DSL（领域特定语言）
- Agent 自我修改 SOUL 文件的能力（需严格权限控制）
- 多 Agent 环境下的人格一致性保障

## 相关

- [[soul-md]] — Hermes 的 SOUL.md 实现
- [[mercury-agent]] — Mercury 的多文件 soul 方案
- [[hermes-agent]] — 两个实现的目标平台之一
- [[hindsight-memory]] — Hermes 记忆方案
- [[mempalace]] — 结构化 AI 记忆系统
