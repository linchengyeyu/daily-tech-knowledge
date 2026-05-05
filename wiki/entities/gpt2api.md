---
title: gpt2api (KleinAI)
created: 2026-05-06
updated: 2026-05-06
type: entity
tags: [ai-tool, deployment, api-gateway, automation]
sources: [session 2026-05-05 weixin]
---

# gpt2api (KleinAI)

## 概述

将 ChatGPT/Grok 等 Web 账户封装为 OpenAI 兼容 API 网关的开源项目，用于个人搭建私有 AI API 服务。

- **GitHub**: https://github.com/432539/gpt2api
- **技术栈**: Go + React + MySQL + Redis
- **部署方式**: Docker Compose
- **端口分配**: 17080(用户前端), 17088(管理后台), 17200(OpenAI兼容API)
- **部署路径**: `/Volumes/DevSSD/gpt2api/`

## 部署经验

### Docker Hub 连接问题

在中国大陆部署时，Docker Hub 拉取镜像会频繁失败（EOF、超时）。解决方案：

1. 配置多个中国镜像源到 `/etc/docker/daemon.json`：
   - `docker.1ms.run`
   - `docker.xuanyuan.me`
   - `docker.rainbond.cc`
2. 单个镜像源不稳定，需配置多个备份
3. 可手动逐个拉取基础镜像缓存本地

### OrbStack 代理问题

**关键发现**: OrbStack 的 Docker daemon 不走系统 VPN 隧道（utun4），导致：
- `docker pull` 失败（daemon 进程无法通过代理）
- `docker run curl` 却能成功（容器内部走宿主网络，继承系统代理）
- 这意味着需要配置镜像源而非依赖代理

### 构建与启动

- 使用 `docker-compose.server.yml`（非 dev-full 版本）
- 共 10 个容器
- MySQL 首次启动可能报 `MYSQL_ONETIME_PASSWORD: unbound variable` 错误，重试可恢复

## ChatGPT Session Token 获取

从浏览器获取 ChatGPT 会话令牌：
1. 打开 chatgpt.com 并登录
2. F12 → Application → Cookies
3. 复制 `__Secure-next-auth.session-token` 的值

## 相关

- [[open-webui]] — Open WebUI 可通过 gpt2api 的 OpenAI 兼容接口接入 ChatGPT
- [[hermes-agent]] — Hermes 可配置 gpt2api 作为模型后端
- [[docker-china-mirrors]] — Docker Hub 中国镜像源配置
