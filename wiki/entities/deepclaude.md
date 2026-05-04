---
title: DeepClaude
created: 2026-05-05
updated: 2026-05-05
type: entity
tags: [ai-tool, llm, agent, coding]
sources: [ai-world-digest/2026-05-04]
---

# DeepClaude

开源项目，将 DeepSeek V4 Pro 与 Claude Code Agent 结合，通过 Agent 循环大幅降低 AI 编程成本（号称降低17倍）。

## 基本信息

| 项目 | 值 |
|------|-----|
| 定位 | 低成本 AI 编程 Agent 方案 |
| 核心模型 | DeepSeek V4 Pro（推理） + Claude Code（Agent框架） |
| 成本降幅 | ~17倍（vs 直接使用 Claude） |
| HN 热度 | 142 pts |
| 日期 | 2026-05-04 HN 热榜 |

## 核心思路

- DeepSeek V4 Pro 作为推理引擎，替代昂贵的 Claude/GPT 模型
- 利用 Claude Code 的 Agent 循环能力进行任务编排
- 适合预算有限但需要 Agent 级编程能力的开发者

## 相关

- [[deepseek-protocol-compatibility]] — DeepSeek API 协议兼容性问题
- [[hermes-agent]] — 同样使用 Agent 循环模式的 AI 平台
- [[llm-model-comparison]] — GLM-5.1 vs DeepSeek-V4-Pro 对比
