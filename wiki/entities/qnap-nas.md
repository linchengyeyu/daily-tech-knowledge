---
title: QNAP NAS
created: 2026-04-23
updated: 2026-04-23
type: entity
tags: [company, deployment]
sources: [raw/articles/wula-cloudflare-tunnel-2026.md]
---

# QNAP NAS

## 概述

QNAP（威联通）是网络附加存储（NAS）设备厂商。用户的 NAS 型号部署在家庭网络中（192.168.31.233），提供 SMB 共享、Docker 容器、文件存储等服务。

## 用户环境

- IP：192.168.31.233
- 管理员：admin
- SMB 共享：work、资料、Public、Web、frigate_media、home、Container
- 用途：文件存储、[[cloudflare-tunnel]] 内网穿透、安全资料项目托管

## 相关

- [[cloudflare-tunnel]] 可通过 Docker 部署在 NAS 上实现内网穿透
- [[smb-mount]] macOS 通过 SMB 协议挂载 NAS 共享目录
