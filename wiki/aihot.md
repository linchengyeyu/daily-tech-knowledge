---
title: AIHOT
created: 2026-05-11
updated: 2026-05-11
type: entity
tags:
  - ai-tool
  - automation
  - agent
sources: [conversation/2026-05-10]
---

# AIHOT

AI信源聚合工具，由数字生命卡兹克团队开源，专注AI动态抓取与筛选。

## 基本信息

| 项目 | 详情 |
|------|------|
| 名称 | AIHOT |
| 来源 | 数字生命卡兹克（开源） |
| 网址 | https://aihot.virxact.com |
| 许可 | 完全免费开源，无付费墙 |
| 信源数量 | 160+ |

## 核心功能

- **多源抓取**：覆盖 X（Twitter）、博客、RSS、arXiv 等 160+ 信源
- **AI + 人工打分筛选**：自动抓取后经 AI 和人工双重筛选，输出精选内容
- **三种内容形态**：
  - 精选条目（人工筛选高质量内容）
  - 全部条目（所有抓取内容）
  - 日报（每日 AI 动态汇总）

## API

### 端点

| 端点 | 用途 |
|------|------|
| `/api/public/items` | 获取精选/全部条目 |
| `/api/public/daily` | 获取当日日报 |
| `/api/public/dailies` | 获取日报归档列表 |

### 调用要求

- **必须携带浏览器 User-Agent**，否则返回 403
- 无需 API Key，无需认证

## 自动化集成

- Cron 已配置：每天 8:30 自动拉取精选内容并推送到飞书
- 集成场景：作为 [[ai-world-digest]] 管线的补充信源，或独立使用

## 相关

- [[ai-world-digest]] — AI世界日报自动聚合管线，4源采集
- [[follow-builders]] — AI Builder追踪工具，25个X账号聚合
- [[ai-zhiguanju]] — 公众号内容创作可能使用 AIHOT 作为选题来源
- [[hermes-agent]] — Cron定时任务配置
