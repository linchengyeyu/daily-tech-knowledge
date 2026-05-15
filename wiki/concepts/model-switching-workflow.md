---
title: Hermes 模型切换工作流
created: 2026-05-16
updated: 2026-05-16
type: concept
tags: [configuration, best-practice, hermes]
sources: [conversation/2026-05-15]
---

# Hermes 模型切换工作流

Hermes Agent 的模型切换存在一个关键缺陷及对应的解决方案。

## 问题

使用 `/model` 命令切换模型时，**只更新 `model.default` 字段**，不会同步更新以下关键元数据：

- `base_url` — API 端点地址
- `api_key` — 认证密钥
- `context_length` — 上下文窗口长度

这意味着切换到自定义 provider 的模型后，请求仍会发送到旧的 API 端点，导致调用失败。

## 解决方案：switch_model.py

创建了 `switch_model.py` 脚本，从 `custom_providers` 配置中复制完整的模型元数据：

1. 读取 `config.yaml` 中的 `custom_providers` 定义
2. 找到目标模型的完整配置（base_url、api_key、context_length 等）
3. 将所有字段同步写入当前生效的配置
4. 重启 session 后生效

## Shell Alias

配置了 shell alias `switch` 命令，简化切换流程：

```bash
# 使用 switch 命令快速切换模型
switch <model-name>
```

## 注意事项

- 切换后**必须重启 session** 才能生效
- 适用于自定义 provider 模型（如 DeepSeek、GLM 等）
- 内置模型不受此问题影响

## 相关

- [[hermes-agent]] — Hermes Agent 平台
- [[deepseek-protocol-compatibility]] — DeepSeek 协议兼容性问题
- [[deepseek-fallback-best-practice]] — DeepSeek Fallback 配置实践
