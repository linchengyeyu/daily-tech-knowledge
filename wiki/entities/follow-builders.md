---
title: Follow-Builders
created: 2026-04-29
updated: 2026-04-29
type: entity
tags: [ai-tool, automation, project-doc]
sources: [conversation/2026-04-28]
---

# Follow-Builders

AI Builder 追踪工具，聚合 25 个 X 账号 + 6 个播客 + 2 个博客的 AI 前沿内容。

## 基本信息

| 项目 | 值 |
|------|-----|
| GitHub | `zarazhangrui/follow-builders` (3,515⭐) |
| 语言 | JavaScript (Node.js) |
| 追踪源 | 25 X 账号 + 6 播客 + 2 博客 |

## 公开 Feed 数据

```
https://raw.githubusercontent.com/zarazhangrui/follow-builders/main/feed-x.json
https://raw.githubusercontent.com/zarazhangrui/follow-builders/main/feed-podcasts.json
https://raw.githubusercontent.com/zarazhangrui/follow-builders/main/feed-blogs.json
```

## 追踪的播客

1. Latent Space
2. Training Data
3. No Priors
4. Unsupervised Learning
5. The MAD Podcast
6. AI & I by Every

## 使用方案

不直接安装，而是 **fork 概念**：拉取公开 feed JSON → LLM 摘要 → 推送到公众号「[[ai-zhiguanju]]」+ 飞书 + 微信。利用 [[hermes-agent]] + cron 调度 + 现有 [[wechat-publishing-toolchain]] 实现推送。

## 优势

- 无需配置 X API 或 YouTube 字幕抓取
- 直接使用公开数据，零成本
- 适合定时摘要推送场景

## 相关

- [[ai-zhiguanju]] — 目标发布渠道
- [[hermes-agent]] — 自动化执行引擎
- [[wechat-publishing-toolchain]] — 文章发布工具链
