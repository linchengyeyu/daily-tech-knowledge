---
title: ds4
created: 2026-05-09
updated: 2026-05-09
type: entity
tags: [open-source, ai-tool, local-llm, mac]
sources: [conversation/2026-05-08]
---

# ds4

antirez（Redis 创造者）开发的 Mac 本地 DeepSeek 4 Flash Metal 推理引擎。

## 基本信息

| 项目 | 详情 |
|------|------|
| 作者 | antirez（Salvatore Sanfilippo） |
| 功能 | Mac 上本地运行 DeepSeek 4 Flash 推理 |
| 技术栈 | Metal（Apple GPU 加速） |
| 定位 | 轻量级本地 LLM 推理方案 |

## 关键信息

- 利用 Apple Silicon 的 Metal 框架实现 GPU 加速推理
- 专为 Mac 用户设计，无需云服务即可运行 DeepSeek 模型
- 体现了本地 LLM 推理的趋势：越来越多的工具让用户在个人设备上运行大模型

## 背景

antirez 是 Redis 的原创者，在开源社区有极高影响力。ds4 是他在 AI 推理领域的新尝试，结合了他在系统编程方面的深厚经验和 Apple Metal 的硬件加速能力。

## 相关

- [[ollama]] — 另一个本地 LLM 运行工具
- [[deepseek-protocol-compatibility]] — DeepSeek 协议兼容性
- [[litert-lm]] — Google 端侧大模型推理框架
