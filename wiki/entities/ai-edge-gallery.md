---
title: AI Edge Gallery — Google 端侧 AI 展示应用
created: 2026-05-03
updated: 2026-05-03
type: entity
tags: [ai-tool, llm, model-benchmark]
sources: [raw/articles/guangguang-github-april-hot-2026.md]
---

# AI Edge Gallery

Google 开源的端侧 AI 展示应用，在手机上离线运行大语言模型。

## 功能模块

- **AI Chat**：支持思考模式，可看模型推理过程
- **Ask Image**：图片理解
- **Audio Scribe**：实时语音转录翻译
- **Prompt Lab**：调参数做实验
- **Agent Skills**：模块化技能系统（查 Wikipedia、地图交互等），把 LLM 从纯聊天变成主动助手
- **模型基准测试**：对比不同模型在手机上的性能

## 技术细节

- 基于 [[litert-lm|LiteRT]] 运行时优化
- 最新版支持 Gemma 4 系列模型
- 已上架 Google Play 和 App Store
- Android 12+、iOS 17+

## 链接

- GitHub: https://github.com/google-ai-edge/gallery
- 来源：[[逛逛GitHub 4月热门开源项目]]

## 相关

- [[litert-lm]] — Google 端侧大模型推理框架（底层运行时）
