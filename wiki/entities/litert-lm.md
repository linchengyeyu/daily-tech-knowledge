---
title: LiteRT-LM — Google 端侧大模型推理框架
created: 2026-05-03
updated: 2026-05-03
type: entity
tags: [ai-tool, llm, deployment, model-benchmark]
sources: [raw/articles/guangguang-github-april-hot-2026.md]
---

# LiteRT-LM

Google 推出的端侧大模型推理框架，专为手机、树莓派等资源有限设备优化。

## 应用场景

已用在 Chrome、Chromebook Plus、Pixel Watch 等 Google 自家产品。

## 特性

- **全平台**：Android、iOS、Web、桌面、IoT
- **硬件加速**：GPU 和 NPU 加速
- **多模态**：支持图片等输入
- **Tool Use**：函数调用，可构建端侧 AI Agent 工作流
- **CLI 工具**：一行命令终端跑模型
- 最近新增 Gemma 4 支持

## 模型兼容

Gemma、Llama、Phi-4、Qwen 等主流模型家族

## API

Kotlin、Python、C++ 三种，Swift 开发中

## 链接

- GitHub: https://github.com/google-ai-edge/LiteRT-LM
- 来源：[[逛逛GitHub 4月热门开源项目]]

## 相关

- [[ai-edge-gallery]] — 基于 LiteRT 的端侧 AI 展示应用
