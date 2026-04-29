---
title: Hindsight Memory
created: 2026-04-23
updated: 2026-04-23
type: concept
tags: [ai-tool, agent, best-practice]
sources: [raw/articles/keji-jun-hermes-config-guide-2026.md]
---

# Hindsight Memory

## 概述

Hindsight 是 [[hermes-agent]] 推荐的长期记忆替代方案，取代内置的 MEMORY.md。基于知识图谱自动从每轮对话中提取实体、事实、关系和时间戳，实现无上限的持久记忆。

## 对比内置 MEMORY

| 维度 | 内置 MEMORY | Hindsight |
|------|------------|-----------|
| 写入机制 | Hermes 认为重要时才写入 | 自动从每轮对话提取 |
| 容量上限 | ≈ 2200 字符（硬上限） | 无硬上限 |
| 知识组织 | 线性文本 | 知识图谱 |
| 召回方式 | 注入到 prompt 上下文 | 语义检索 + 图谱遍历 |

## 安装配置

```bash
# 1. 运行 setup wizard
hermes memory setup

# 2. 选择 hindsight

# 3. 获取 API Key（Cloud 模式）
# 打开 https://ui.hindsight.vectorize.io/connect 注册/登录，生成 API Key

# 4. 验证
hermes memory status
```

应看到 Hindsight 已激活，显示 bank_id、auto-recall、auto-retain 等状态。

## 适用场景

- 长期项目：跨会话保持上下文，不用每次重新交代背景
- 多领域工作：自动分类存储不同领域的知识
- 知识管理：与 [[llm-wiki-pattern]] 互补，Hindsight 管对话记忆，Wiki 管编译知识

## 相关

- [[hermes-agent]] — Hindsight 是 Hermes 的记忆插件
- [[llm-wiki-pattern]] — 另一种知识管理方式，侧重编译而非记忆
