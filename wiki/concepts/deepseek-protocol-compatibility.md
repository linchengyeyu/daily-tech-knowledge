---
title: DeepSeek 协议兼容性
created: 2026-04-29
updated: 2026-05-05
type: concept
tags: [llm, deployment, best-practice]
sources: [conversation/2026-04-28, conversation/2026-04-29]
---

# DeepSeek 协议兼容性

DeepSeek API 同时支持 OpenAI 和 Anthropic 协议，但在作为 [[hermes-agent]] 回退模型时有兼容性陷阱。

## 问题（HTTP 400 "thinking must be passed back"）

当 GLM-5.1 因 429 限流触发回退到 `deepseek-v4-flash` 时，请求失败并返回：

```
HTTP 400: {"message": "thinking must be passed back"}
```

## 根因（三重问题）

此次问题有 **三个叠加原因**：

1. **错误的 `base_url`**：配置指向了 DeepSeek 的 Anthropic 端点 `https://api.deepseek.com/anthropic`
2. **错误的 `api_mode`**：设为 `anthropic_chat` 而非 `openai_chat`，导致消息经过 Anthropic adapter 处理
3. **`anthropic_adapter.py` 剥离 thinking blocks**：该 adapter 的 `convert_messages_to_anthropic()` 函数会过滤非 Anthropic 格式的 thinking blocks，导致发送给 DeepSeek 的对话历史中 thinking 内容丢失

DeepSeek 检测到历史中有 thinking 请求但无 thinking 回复，于是拒绝请求。

## 完整修复方案

需要 **同时** 做三项修改：

### 1. 修改 `base_url`

```yaml
# 错误 ❌
base_url: https://api.deepseek.com/anthropic

# 正确 ✅
base_url: https://api.deepseek.com
```

### 2. 修改 `api_mode`

```yaml
# 错误 ❌
api_mode: anthropic_chat

# 正确 ✅
api_mode: openai_chat
```

### 3. 补丁 `anthropic_adapter.py`（防御性修复）

在 `anthropic_adapter.py` 中增加 DeepSeek 检测，对 DeepSeek 来源的请求保留 thinking blocks 不做过滤：

```python
# 检测是否为 DeepSeek 端点，保留 thinking blocks
if "deepseek" in base_url:
    # 跳过 thinking block 过滤
    pass
```

### 最终配置

```yaml
# ~/.hermes/config.yaml
fallback_models:
  - model: deepseek-v4-flash
    base_url: https://api.deepseek.com      # OpenAI 协议
    api_mode: openai_chat
    api_key: sk-xxx
    max_tokens: 384000
    fallback_on: [429, 529, 503, connection_error]
```

## 教训

1. 多协议 API 选用时要注意 adapter 层的消息转换行为
2. **三个配置必须同时修改**：仅改 `base_url` 不改 `api_mode` 仍会走 Anthropic adapter
3. Hermes `redact_secrets: true` 会遮蔽 config.yaml 中的 API key，调试时需用 Python 绕过
4. `/model` 菜单已内置 DeepSeek provider（`deepseek-chat`、`deepseek-reasoner`），使用 OpenAI 协议 `https://api.deepseek.com/v1`
5. HTTP 400 错误不一定是你请求错了——可能是中间层（adapter）篡改了你的消息

## 相关

- [[hermes-agent]] — Agent 平台，触发回退机制
- [[llm-model-comparison]] — GLM-5.1 vs DeepSeek 对比
- [[ai-world-digest]] — 使用 DeepSeek 模型的内容管线
- [[deepseek-fallback-best-practice]] — 基于本文的完整 fallback 配置最佳实践（含公众号教程文章）
