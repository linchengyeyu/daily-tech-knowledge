---
title: ima2-gen
created: 2026-05-16
updated: 2026-05-16
type: entity
tags: [ai-tool, image-generation, api]
sources: [conversation/2026-05-15]
---

# ima2-gen

ChatGPT 网页生图 API 封装工具，将 ChatGPT gpt-image-2 生图能力封装为本地 API。

## 基本信息

- **项目**：[lidge-jun/ima2-gen](https://github.com/lidge-jun/ima2-gen)
- **Stars**：⭐213
- **功能**：将 ChatGPT 网页端的 gpt-image-2 生图能力封装为本地可调用的 API 接口
- **用途**：无需 OpenAI API Key，直接利用 ChatGPT 网页登录态生图

## 常见失败原因

| 失败原因 | 说明 |
|----------|------|
| OAuth 过期 | ChatGPT 登录态过期，需重新获取 OAuth token |
| 额度限流 | ChatGPT 网页端有生图频率/数量限制 |
| Cloudflare 403 | Cloudflare 反爬拦截，需处理 challenge |
| SSE 解析失败 | Server-Sent Events 流式响应解析异常 |

## 相关

- [[gpt2api]] — 类似思路，将 ChatGPT 账户封装为 OpenAI 兼容 API
- [[hermes-agent]] — 可通过 API 调用集成生图能力
