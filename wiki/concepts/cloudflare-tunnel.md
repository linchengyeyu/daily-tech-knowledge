---
title: Cloudflare Tunnel
created: 2026-04-23
updated: 2026-04-23
type: concept
tags: [deployment, tutorial, best-practice]
sources: [raw/articles/wula-cloudflare-tunnel-2026.md]
---

# Cloudflare Tunnel

## 概述

Cloudflare Tunnel 是 Cloudflare 提供的免费内网穿透方案。无需公网 IP、不用端口映射、不暴露路由器，通过在本地运行 cloudflared 客户端建立出站连接到 Cloudflare 边缘网络，实现从外网安全访问内网服务。

## 核心优势

- **零成本**：Cloudflare 免费套餐即可使用
- **安全性高**：不暴露内网真实 IP 和端口，所有流量经 Cloudflare 代理
- **配置简单**：一条 docker 命令即可启动

## 主要缺点

- **国内访问慢**：流量绕经 Cloudflare 海外节点，延迟高
- **需要域名**：域名必须托管到 Cloudflare DNS

## 部署方式

### Docker 部署（推荐）

```bash
docker run cloudflare/cloudflared:latest tunnel --protocol http2 --no-autoupdate run --token <TOKEN>
```

国内用户加 `--protocol http2` 可加快连接速度。

### 飞牛OS应用商店（不推荐）

版本较低，无法查看日志，操作反而更复杂。

## 加速方案

通过自定义主机名 + CNAME 优选IP 实现国内加速访问：

1. 准备第二个域名托管到 CF（加速专用）
2. 在隧道中添加加速域名的路由
3. 设置回退源 → 添加自定义主机名 → DNS验证 → 证书验证
4. 配置 DCV 委派实现证书自动续费
5. 加速域名添加优选IP记录（如 `www.visa.cn`）
6. 主域名 CNAME 指向加速域名

加速后延迟大幅降低，应用类服务也可正常使用。

## 替代方案对比

| 方案 | 需要公网IP | 安全性 | 国内速度 | 成本 |
|------|-----------|--------|---------|------|
| [[cloudflare-tunnel]] | 否 | 高 | 慢（需加速） | 免费 |
| Lucky + DDNS | 需IPv6 | 中（暴露端口） | 快 | 免费 |
| FRP | 否 | 中 | 快 | 需服务器 |

## 相关

- 适用于 [[qnap-nas]] 等 NAS 设备的内网穿透
- 对比传统 [[lucky-ddns]] 方案
