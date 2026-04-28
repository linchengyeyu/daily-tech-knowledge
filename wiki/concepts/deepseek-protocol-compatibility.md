---
title: DeepSeek 协议兼容性
created: 2026-04-29
updated: 2026-04-29
type: concept
tags: [llm, deployment, best-practice]
sources: [conversation/2026-04-28]
---

# DeepSeek 协议兼容性

DeepSeek API 同时支持 OpenAI 和 Anthropic 协议，但在作为 [[hermes-agent]] 回退模型时有兼容性陷阱。

## 问题

当 DeepSeek 配置为 Anthropic 协议（`base_url: https://api.deepseek.com/anthropic`）时，如果主模型（如 glm-5.1）因 429 限流触发回退，对话历史中包含的 thinking blocks 会被 [[hermes-agent]] 的 `anthropic_adapter.py` 剥离，导致 DeepSeek 返回 HTTP 400 错误。

## 根因

`anthropic_adapter.py` 的 `convert_messages_to_anthropic()` 函数会过滤非 Anthropic 格式的 thinking blocks，导致发送给 DeepSeek 的请求格式不完整。

## 解决方案

将 `base_url` 从 `https://api.deepseek.com/anthropic` 改为 `https://api.deepseek.com`（走 OpenAI 协议），避免 Anthropic adapter 干扰。

## 关键配置

```yaml
# ~/.hermes/config.yaml
fallback_models:
  - model: deepseek-v4-flash
    base_url: https://api.deepseek.com    # OpenAI 协议
    api_key: sk-xxx
    max_tokens: 384000
    fallback_on: [429, 529, 503, connection_error]
```

## 教训

1. 多协议 API 选用时要注意 adapter 层的消息转换行为
2. Hermes `redact_secrets: true` 会遮蔽 config.yaml 中的 API key，调试时需用 Python 绕过
3. `/model` 菜单已内置 DeepSeek provider（`deepseek-chat`、`deepseek-reasoner`），使用 OpenAI 协议 `https://api.deepseek.com/v1`

## 相关

- [[hermes-agent]] — Agent 平台，触发回退机制
- [[llm-model-comparison]] — GLM-5.1 vs DeepSeek 对比
