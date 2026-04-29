---
title: 微信 iLink Token 过期机制
created: 2026-04-25
updated: 2026-04-25
type: concept
tags: [automation, best-practice]
sources: [session:2026-04-24-xianyu-monitor]
---

# 微信 iLink Token 过期机制

## 问题
通过 Hermes 的 iLink 网关向微信发送消息时，API Token 会在约 7 天后过期。过期后所有微信推送失败（返回 `ret=-2`）。

## 表现
- cron job 日志显示 WeChat delivery FAILED
- 错误码：`ret=-2`（token 无效/过期）
- 飞书渠道不受影响

## 解决方案
```bash
hermes gateway setup → 选择 Weixin → 扫码重新绑定
```
重新扫码后 Token 刷新，可继续使用约 7 天。

## 影响范围
- [[xianyu-monitor]] — 每日播报无法推送到微信
- [[hermes-agent]] — 所有依赖微信推送的自动化任务

## 最佳实践
- 将 Token 刷新纳入定期维护流程（每周一次）
- 飞书作为备用推送渠道，确保消息不丢失
- 可考虑 Token 到期前主动提醒

## 相关页面
- [[xianyu-monitor]] — 受此问题影响的监控系统
- [[hermes-agent]] — Hermes Agent 平台
