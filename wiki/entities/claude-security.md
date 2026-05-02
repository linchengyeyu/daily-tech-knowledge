---
tags: [security, ai-tools, anthropic, code-audit]
related: [hermes-agent, opencli]
last_updated: 2026-05-03
---

# Claude Security

> Anthropic 推出的 AI 代码安全审计工具，基于 Claude Opus 4.7 构建。

## 基本信息

- **开发者**: Anthropic
- **发布时间**: 2026年5月2日（公开测试版）
- **类型**: AI 代码安全审计工具
- **官网**: https://claude.ai/security

## 核心功能

- **无需 API**：安全团队无需搭建自定义工具即可在代码仓库中发现漏洞
- **集成 Claude Code Web**：指向仓库即可获得经验证的漏洞发现并在同一界面修复
- **企业级功能**：目录级扫描、CSV导出、Webhook告警、定时扫描
- **生产就绪**：数百个组织已在生产代码上使用

## 技术细节

- 基于 Claude Opus 4.7 模型
- 支持漏洞发现 + 修复在同一界面完成
- 已集成到 Claude Code 网页版
- 提供 Webhook 通知机制，适合 CI/CD 集成

## 意义

标志着 AI 安全工具从"安全研究"走向"工程实战"，开发者不再需要专门的安全团队就能进行代码安全审计。与 OpenClaw 联合 NVIDIA、OpenAI、微软推进安全生态的方向一致。

## 来源

- 2026-05-02 AI世界日报（Claude 官方推特 @claudeai 发布）
