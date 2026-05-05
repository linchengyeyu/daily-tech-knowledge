---
title: Open WebUI
created: 2026-04-25
updated: 2026-05-06
type: entity
tags: [ai-tool, deployment, llm]
sources: [session:2026-04-24-open-webui-timeout, session:2026-05-05-weixin]
---

# Open WebUI

## 概述
Open WebUI 是一个开源的 LLM Web 前端，支持连接多种后端（Ollama、OpenAI 兼容 API 等）。在本地 Docker 环境中运行，端口 7530。

## 关键配置

### 超时设置
- **问题**：复杂 AI Agent 任务（如 Hermes）超过默认 5 分钟超时
- **根因**：`AIOHTTP_CLIENT_TIMEOUT` 默认为 `None`，aiohttp 实际使用 300 秒（5分钟）
- **解决方案**：Docker 创建时设置环境变量 `AIOHTTP_CLIENT_TIMEOUT=600`（10分钟）

```bash
docker run -d --name open-webui -p 7530:8080 \
  -e AIOHTTP_CLIENT_TIMEOUT=600 \
  -e OPEN_WEBUI_AUTH=TRUE \
  -v open-webui:/app/backend/data \
  --restart always \
  ghcr.io/open-webui/open-webui:main
```

### 运行环境
- Docker 容器名：`open-webui`
- 端口映射：`7530:8080`
- 数据卷：`open-webui` → `/app/backend/data`
- Ollama 连接错误可忽略（未安装 Ollama）

## 踩坑记录
- 2026-04-24：超时问题导致 Hermes 长任务无法完成，通过设置 `AIOHTTP_CLIENT_TIMEOUT=600` 解决
- 2026-05-05：账户创建踩坑 — 需在 `auth` 和 `user` 两张 SQLite 表都插入记录才能正常登录
- 2026-05-05：间歇性断连 — 添加 `ENABLE_WEBSOCKET_SUPPORT=true` 和 `WEBSOCKET_RECONNECT_TIMEOUT=60`
- 2026-05-05：Open WebUI 不支持显示 Agent 中间工具调用过程（只能看到最终文本输出），这是架构限制

## gpt2api 集成

可通过 [[gpt2api]] 将 ChatGPT Web 账户封装为 OpenAI 兼容 API，然后在 Open WebUI 中添加为模型后端。

## 相关页面
- [[hermes-agent]] — 通过 Open WebUI 作为前端使用
- [[ai-zhiguanju]] — 公众号写作中使用 Open WebUI 调用 AI
- [[gpt2api]] — ChatGPT 账户封装为 OpenAI 兼容 API
- [[docker-china-mirrors]] — Docker Hub 中国镜像配置
