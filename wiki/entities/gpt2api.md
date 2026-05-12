---
title: gpt2api (KleinAI)
created: 2026-05-06
updated: 2026-05-13
type: entity
tags: [ai-tool, deployment, api-gateway, automation]
sources: [session 2026-05-05 weixin, session 2026-05-11 weixin, feishu/2026-05-12]
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

## Mock Mode Bug（2026-05-11 发现）

`docker-compose.dev-full.yml` 中 `KLEIN_PROVIDER_GPT: mock` 和 `KLEIN_PROVIDER_GROK: mock` 导致 API 一直返回假数据。

- 即使 `docker-compose.server.yml` 定义为 `real`，dev-full 的 YAML anchor 优先级更高，覆盖了 server 的配置
- **修复**：改 `docker-compose.dev-full.yml` 第33-34行为 `real`

## Docker 容器代理配置（2026-05-11 发现）

容器默认没有 `HTTP_PROXY` / `HTTPS_PROXY` 环境变量，无法访问 chatgpt.com 等外部服务。

- OrbStack Docker daemon 的代理配置（`~/.orbstack/config/docker.json`）只影响 image pull，**不影响容器运行时**
- **修复**：在 `x-backend-env` / `x-common-env` 中添加：
  ```yaml
  HTTP_PROXY: http://192.168.31.165:7890
  HTTPS_PROXY: http://192.168.31.165:7890
  NO_PROXY: localhost,127.0.0.1,mysql,redis,...
  ```
- 修复后容器内 `curl chatgpt.com` 从 403 变为 308（成功）
- 代理来源：[[proxytunnel]] Chrome 扩展监听 `*:7890`

## 端口与网络信息

| 服务 | 端口 |
|------|------|
| 用户前端 | 17080 |
| 管理后台 | 17088 |
| OpenAI 兼容 API | 17200 |
| Admin API | 17188 |
| User API | 17180 |
| FlareSolverr | 18191 |

- 容器网络：`klein-dev-net`

## Provider Factory 代码位置

- `backend/internal/provider/factory/factory.go`

## 2026-05-12 飞书会话记录（session 20260512_181055）

继续调试 gpt2api 的 mock mode 和 proxy 问题：
- 确认 Mock Mode 在 dev-full → server 切换后的配置一致性
- 验证容器运行时代理（HTTP_PROXY/HTTPS_PROXY）的实际连通性
- ChatGPT session token 的有效性检查

## 未解决问题

- ChatGPT session token 过期需要重新导入
- FlareSolverr 返回 502，`grok_cf_refresh` 失败
- 代理依赖 [[proxytunnel]] Chrome 扩展持续运行，扩展关闭则代理不可用

## 相关

- [[open-webui]] — Open WebUI 可通过 gpt2api 的 OpenAI 兼容接口接入 ChatGPT
- [[hermes-agent]] — Hermes 可配置 gpt2api 作为模型后端
- [[docker-china-mirrors]] — Docker Hub 中国镜像源配置
- [[proxytunnel]] — ProxyTunnel Chrome 代理扩展，提供容器运行时代理
