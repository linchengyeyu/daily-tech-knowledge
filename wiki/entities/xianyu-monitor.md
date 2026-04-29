---
title: 闲鱼监控 (Goofish Monitor)
created: 2026-04-25
updated: 2026-04-25
type: entity
tags: [ai-tool, automation, deployment]
sources: [session:2026-04-24-xianyu-monitor]
---

# 闲鱼监控 (Goofish Monitor)

## 概述
本地运行的闲鱼（Goofish/咸鱼）商品监控工具，自动扫描指定关键词的商品，通过 AI 分析筛选值得购买的二手好物。Web 管理界面运行在 `http://127.0.0.1:8000`，默认管理员 `admin/admin123`。

## 关键功能
- 定时扫描指定关键词商品（如 "mac studio"）
- AI 自动分析商品描述，判断是否值得购买
- 每日播报（cron job 早/晚各一次）
- 结果推送至飞书和微信

## 运行数据（截至 2026-04-24）
- 监控关键词：`mac studio`
- 每次扫描约 20-26 件商品
- 当前均价：¥3,712（24 个样本）
- 历史均价：¥2,307（271 个唯一商品）
- **持续零推荐**：4月20日-24日每日均为 0 推荐

## 已知问题

### 搜索关键词太宽泛
- "mac studio" 会匹配到 MacBook Air/Pro、Mac mini、配件等不相关商品
- 建议：精确化搜索关键词，如 "Mac Studio M2 Max" 或使用排除词

### AI 分析空响应
- 每次扫描约 5-6 件商品出现"AI响应内容为空"错误
- 可能是 API 调用超时或 rate limit

### 推送渠道问题
- **微信 iLink Token 过期**：约 7 天过期，需手动扫码刷新（`hermes gateway setup` → Weixin）
- **飞书推送正常**：作为备用渠道稳定运行
- 详见 [[wechat-ilink-token]]

## Cron 配置
- Job ID: `b6cc321af63e`
- 早间播报：约 7:35 AM
- 晚间播报：21:00 PM
- 当 `send_message` 工具不可用时，cron job 无法自动推送

## 相关页面
- [[hermes-agent]] — 运行监控任务的 AI Agent
- [[wechat-ilink-token]] — 微信推送 Token 过期问题
