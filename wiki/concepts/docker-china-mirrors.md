---
title: Docker Hub 中国镜像源配置
created: 2026-05-06
updated: 2026-05-06
type: concept
tags: [deployment, best-practice, docker]
sources: [session 2026-05-05 weixin]
---

# Docker Hub 中国镜像源配置

## 问题

在中国大陆直接拉取 Docker Hub 镜像（registry-1.docker.io）会频繁遇到：
- EOF 错误
- 超时
- 429 Rate Limit

## 解决方案

### 1. 配置镜像加速源

在 `/etc/docker/daemon.json`（OrbStack 中通过设置界面修改）添加：

```json
{
  "registry-mirrors": [
    "https://docker.1ms.run",
    "https://docker.xuanyuan.me",
    "https://docker.rainbond.cc"
  ]
}
```

**注意**: 单个镜像源不稳定，必须配置多个备份。镜像源可能随时失效，需定期更新。

### 2. 手动预拉取基础镜像

构建项目前，先手动拉取所需基础镜像：

```bash
docker pull golang:1.24-alpine
docker pull nginx:1.27-alpine
docker pull node:20-alpine
docker pull mysql:8.0
docker pull redis:7-alpine
docker pull caddy:2-alpine
```

逐个拉取比 `docker compose build` 一次性拉取成功率更高。

### 3. OrbStack 代理陷阱

**关键**: OrbStack 的 Docker daemon 进程不走系统 VPN 隧道（utun4），即使系统配置了代理：
- `docker pull` → daemon 发起请求 → 不走代理 → 直连失败
- `docker run curl google.com` → 容器内进程 → 走宿主网络 → 继承系统代理 → 成功

因此在中国使用 OrbStack 时，**必须配置镜像加速源**，不能依赖代理。

### 4. 429 限流应对

当镜像源返回 429（请求过于频繁）：
- 降低并发，逐个拉取
- 等待几分钟后重试
- 切换到其他镜像源

## 相关

- [[open-webui]] — Open WebUI Docker 部署踩坑
- [[gpt2api]] — gpt2api 部署中的 Docker 镜像拉取问题
- [[cloudflare-tunnel]] — 内网穿透方案
