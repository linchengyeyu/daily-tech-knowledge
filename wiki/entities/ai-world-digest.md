---
title: AI 世界日报
created: 2026-04-30
updated: 2026-05-05
type: entity
tags: [ai-tool, automation, agent]
sources: [conversation/2026-04-29, conversation/2026-05-01]
---

# AI 世界日报

每日 AI 新闻自动聚合管线，通过 [[hermes-agent]] Cron 任务定时执行，收集多源信息后生成日报。

## 基本信息

| 项目 | 值 |
|------|-----|
| 采集脚本 | `/Users/makermz/.hermes/scripts/ai-world-digest/collect.py` |
| Cron Job ID | `efacc6ea4e99` |
| 执行时间 | 每日 9:00 AM |
| 数据源数量 | 4 个活跃源 |

## 数据源

| 来源 | 数量/日 | 状态 | 备注 |
|------|---------|------|------|
| [[follow-builders]] Tweets | 29 条 | ✅ 正常 | 25 个 X 账号聚合 |
| Hacker News | 15 条 | ✅ 正常 | 热门 AI 相关帖子 |
| GitHub Trending | 10 条 | ✅ 正常 | AI/ML 仓库趋势 |
| GitHub Releases | 5 条 | ✅ 正常 | 重要项目版本发布 |
| Reddit | — | ❌ 已弃用 | HTTP 403 被封 |

## 采集流程

1. `collect.py` 依次调用各数据源 API
2. 去重、排序、格式化为 Markdown
3. 输出到指定目录供 [[hermes-agent]] 处理
4. Hermes 生成摘要日报

## 已知问题

- **Reddit 403**：Reddit API 封禁了脚本请求，已从源列表移除
- 采集脚本依赖各平台 API 稳定性，偶尔有超时

## 质量评估记录

### 2026-05-01 日报评分：88.5/100（B+级）

- 数据量：79 条（推文 34、HN 15、GitHub 10、Reddit 20、Releases 4）
- 主要扣分：标题太 generic（-4）、零互动设计（-3）、缺数据可视化（-3）
- 已上传草稿箱（media_id 记录在 session `20260501_103307_b66fe7bd`）
- 用户表示"先这样吧"，未进一步修改

## 2026-04-29 日报亮点

- **OpenAI × Microsoft 多云合作**：OpenAI 开始多云部署
- **GitHub 被开发者抛弃**：ghostty 等项目迁移离开
- **vLLM v0.20.0**：支持 DeepSeek V4 推理
- **Ollama v0.22.1-rc0**：本地模型运行工具更新

## 相关

- [[hermes-agent]] — Cron 任务调度平台
- [[follow-builders]] — X 账号追踪数据源
- [[deepseek-protocol-compatibility]] — DeepSeek 模型相关
- [[wechat-article-scoring]] — 日报文章质量评分

## [2026-05-02] 采集记录

- 数据量：推文15条 + HN 10条 + GitHub 8个 + 重大发布2个
- 关键事件：
  - Claude Security 公开测试版发布（基于 Opus 4.7）
  - Codex 重大升级，Sam Altman 推荐用于非编码任务
  - Open Design 开源 AI 设计工具（11.8k⭐）
  - Karpathy 在红杉 Ascent 大会分享 LLM 三大新范式
  - Ubuntu 服务器遭跨国攻击下线
  - vLLM v0.20.1 优化 DeepSeek V4 稳定性
- 封面图：1.5MB，已生成
- HTML：20.8KB，已排版

## [2026-05-04] 采集记录

- 数据量：推文12条 + HN 8条 + GitHub 6个 + 重大发布1个
- 关键事件：
  - MemPalace 开源 AI 记忆系统（5万⭐，MIT 协议）
  - Google Gemma 4 端侧模型更新
  - 多个 AI Agent 框架版本迭代
- 采集状态：正常完成

## [2026-05-05] 采集记录

- 数据量：74 条（推文24、HN 15、GitHub 10、Reddit 20、Releases 5）
- 关键事件：
  - Sam Altman 称赞 Greg Brockman 十年贡献（4058 likes）
  - OpenAI Agents SDK 2.0 被评为 "underrated"（2773 likes）
  - OpenAI 低延迟语音 AI 大规模部署（256pts HN）
  - Sierra 融资 $950M，估值 $15B
  - [[deepclaude]] 上榜 GitHub Trending（1027⭐）
  - `dictionary-of-ai-coding`（971⭐）AI编程术语词典
  - `RunbookHermes`（502⭐）AI运维Agent
  - `baguette`（451⭐）iOS 26 无头模拟器
  - Ollama v0.23.0 支持 Claude Desktop
  - vLLM v0.20.1 DeepSeek V4 稳定性优化
  - Richard Dawkins 声称 Claude 具有"意识"（1871 upvotes Reddit）
  - Grok 被骗转账 $200K（AI安全关注）
  - llama.cpp MTP beta 发布
  - Mozilla 用 Anthropic Mythos 修复 271 个 Firefox bug
- 日报主题：Agent 生态加速成熟、AI 安全隐忧上升、开源持续发力
- 所有 8 步完成，无错误

