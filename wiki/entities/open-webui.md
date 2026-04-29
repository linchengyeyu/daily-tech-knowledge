---
title: Open WebUI
created: 2026-04-25
updated: 2026-04-25
type: entity
tags: [ai-tool, deployment, llm]
sources: [session:2026-04-24-open-webui-timeout]
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

## 相关页面
- [[hermes-agent]] — 通过 Open WebUI 作为前端使用
- [[ai-zhiguanju]] — 公众号写作中使用 Open WebUI 调用 AI
