---
title: Ollama
created: 2026-05-05
updated: 2026-05-05
type: entity
tags: [ai-tool, llm, deployment]
sources: [ai-world-digest/2026-05-04]
---

# Ollama

本地大语言模型运行工具，一条命令即可在本地跑各种开源模型。2026年5月发布 v0.23.0 重磅更新。

## 基本信息

| 项目 | 值 |
|------|-----|
| GitHub | `ollama/ollama` |
| 最新版本 | v0.23.0（2026-05-04） |
| 定位 | 本地 LLM 运行和管理 |
| 支持平台 | macOS / Linux / Windows |

## v0.23.0 重大更新

- **Claude Desktop 集成**：通过 `ollama launch claude-desktop` 一行命令即可配置
- 支持 Claude Cowork 和 Claude Code 模式
- 本地模型 + Claude 桌面端的无缝衔接

## 常用场景

- 本地运行开源模型（Llama、Gemma、DeepSeek 等）
- 隐私敏感场景下的 AI 推理
- 开发测试环境中的模型评估
- 配合 [[vllm]] 等框架进行模型服务

## 相关

- [[deepseek-protocol-compatibility]] — DeepSeek 模型相关
- [[deepclaude]] — 模型组合优化方案
