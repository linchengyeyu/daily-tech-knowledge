---
title: AIHOT
created: 2026-05-11
updated: 2026-05-17
type: entity
tags:
  - ai-tool
  - automation
  - agent
sources: [conversation/2026-05-10, AIHOT速报/2026-05-12, AIHOT速报/2026-05-13, AIHOT速报/2026-05-16]
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

## AIHOT 速报精选（2026-05-12）

当日 AIHOT 速报关键动态：

1. **[[chatgpt-5-5-pro]] 解菲尔兹奖级别数学题** — OpenAI 高端模型数学推理能力重大突破
2. **[[anthropic-valuation]] 估值达 1.4 万亿** — AI 安全导向公司获资本市场高度认可
3. **[[small-model-orchestration|7B 模型指挥大模型]]** — AI 权力倒挂新范式：小模型做规划，大模型做执行
4. **[[deepseek-v4-pro]] 排名第一** — DeepSeek V4 Pro 在推理模型排行榜登顶

## AIHOT 速报精选（2026-05-13）

当日 AIHOT 速报关键动态：

1. **[[claude-opus-4-7]] Fast Mode 研究预览发布** — Anthropic 最新模型，API + Claude Code 双渠道可用
2. **[[step-image-edit-2]] 登顶 KRIS-Bench** — 3.5B 参数图像编辑模型，在权威基准测试中排名第一
3. **[[google-android-intelligence]] 跨应用自动化** — Google Android AI 智能功能，支持跨应用多步操作和 AI 增强鼠标指针
4. **[[ai-seeding-note-lawsuit|AI 种草笔记首案]]** — 中国首例 AI 生成种草笔记诉讼，工具提供方被判赔 10 万 RMB
5. **[[statewright-ai-constraint|Statewright 方法论]]** — 状态机约束将 AI Agent 准确率从 2/10 提升到 10/10

## API 字段说明

- **无 score 字段**：API 返回数据中不包含 score 评分字段
- **mode=selected**：精选条目通过 `mode=selected` 参数获取，代表人工筛选的高质量内容

## AIHOT 速报精选（2026-05-16）

当日 AIHOT 速报关键动态：

1. **[[lark-cli|飞书 Lark CLI]] 开源破万星** — 45 天 GitHub 破万星，国内首个破万星办公套件开源项目，允许 AI 通过命令行直接操作飞书（score 85）
2. **[[anthropic-valuation-2026|Anthropic 估值飙升至 $900B]]** — 3 个月估值飙升，ARR 达 $45B（score 95）
