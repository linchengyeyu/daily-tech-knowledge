---
title: ProxyTunnel
created: 2026-05-11
updated: 2026-05-11
type: entity
tags: [proxy, chrome-extension, networking, docker]
sources: [session 2026-05-11 weixin]
---

# ProxyTunnel

## 概述

ProxyTunnel 是 Nextin 开发的 Chrome 代理扩展，在 macOS 上创建系统级 VPN 隧道，为本地应用和 Docker 容器提供网络代理。

- **监听端口**：7890（host IP `192.168.31.165`）
- **类型**：系统级 VPN 隧道（utun4），不是标准 HTTP 代理
- **用途**：给 Docker 容器提供 chatgpt.com 等外部服务访问

## 关键特性

- Chrome 浏览器扩展，需在 Chrome 中运行
- 监听 `*:7890` 端口，可被容器通过 host IP 访问
- 创建 utun4 系统级 VPN 隧道，非传统 HTTP/SOCKS 代理

## 用途：Docker 容器代理

在 [[gpt2api]] (KleinAI) 部署中，容器需要访问 chatgpt.com 获取 API 数据。配置方法：

```yaml
# 在 docker-compose 的 x-backend-env / x-common-env 中添加
HTTP_PROXY: http://192.168.31.165:7890
HTTPS_PROXY: http://192.168.31.165:7890
NO_PROXY: localhost,127.0.0.1,mysql,redis,...
```

修复后容器内 `curl chatgpt.com` 从 403 变为 308（成功）。

## 局限性

- **Chrome 扩展依赖**：Chrome 浏览器必须保持运行，扩展关闭则代理不可用
- **非标准代理**：基于 utun4 VPN 隧道，不是标准 HTTP 代理协议
- **单点故障**：代理服务依赖单个 Chrome 扩展进程

## 相关

- [[gpt2api]] — 使用 ProxyTunnel 提供容器运行时代理
- [[docker-china-mirrors]] — Docker Hub 中国镜像源配置（解决 image pull 问题）
