---
title: Statewright AI 约束方法论
created: 2026-05-14
updated: 2026-05-14
type: concept
tags:
  - ai-agent
  - methodology
  - state-machine
  - reliability
  - engineering
sources: [conversation/2026-05-13]
---

# Statewright AI 约束方法论

用状态机（State Machine）约束 AI Agent 行为的方法论，将任务准确率从 2/10 提升到 10/10。

## 核心理念

| 项目 | 详情 |
|------|------|
| 方法名 | Statewright |
| 核心技术 | 状态机（Finite State Machine） |
| 效果 | 准确率 2/10 → 10/10 |
| 适用场景 | AI Agent 任务编排与执行 |

## 问题背景

AI Agent 在执行复杂多步任务时，常见问题包括：

- **幻觉漂移**：Agent 在多步执行中逐渐偏离原始目标
- **不可控分支**：自由格式提示词导致 Agent 行为不可预测
- **重复失败**：相同任务多次执行，结果不一致

## Statewright 方案

### 状态机约束

- **定义有限状态**：将任务拆解为明确的、有限的状态集合
- **定义合法转换**：只允许预定义的状态间转换路径
- **定义约束条件**：每个状态的进入/退出条件明确

### 效果对比

| 指标 | 无约束 | Statewright 约束 |
|------|--------|------------------|
| 任务准确率 | 2/10 | 10/10 |
| 行为可预测性 | 低 | 高 |
| 调试难度 | 高 | 低（状态路径可追溯） |
| Token 消耗 | 不稳定 | 可控 |

## 与其他方法论的对比

- **vs [[agent-soul-architecture|SOUL 架构]]**：SOUL 定义人格，Statewright 定义行为边界；两者互补
- **vs [[karpathy-llm-paradigms|Karpathy .md 范式]]**：.md 文件提供指令，Statewright 提供结构化约束
- **vs [[small-model-orchestration|小模型指挥大模型]]**：Statewright 侧重约束结构，小模型侧重任务分解

## 实践启示

- AI Agent 不是越自由越好，结构化约束能显著提升可靠性
- 状态机是软件工程经典方法论，在 AI 时代依然有效
- 适合需要高可靠性的自动化场景（如 [[hseffyun-spider|爬虫]]、[[ai-world-digest|日报管线]]）

## 相关

- [[agent-soul-architecture]] — Agent SOUL 架构概念
- [[karpathy-llm-paradigms]] — Karpathy LLM 三大新范式
- [[small-model-orchestration]] — 小模型指挥大模型范式
- [[generic-agent]] — 开源 AI Agent 框架
- [[mercury-agent]] — Soul-driven 轻量 AI Agent
