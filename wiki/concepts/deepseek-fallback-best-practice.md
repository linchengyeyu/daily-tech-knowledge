---
title: DeepSeek Fallback 配置最佳实践
created: 2026-05-05
updated: 2026-05-05
type: concept
tags: [llm, deployment, best-practice, automation]
sources: [conversation/2026-05-04]
---

# DeepSeek Fallback 配置最佳实践

以 GLM-5.1 为主力、DeepSeek V4 Flash 为备用的自动切换方案，实现 AI 服务高可用。

## 架构

```
你的请求 → Hermes Agent → 主模型（GLM-5.1，免费）
                              ↓ 429/529/503/连接失败
                           备用模型（DeepSeek V4 Flash，¥1-2/百万token）
                              ↓ 自动恢复
                           回到主模型
```

### 触发条件

| HTTP 状态码 | 含义 |
|-------------|------|
| 429 | 限流（Too Many Requests） |
| 529 | 服务过载 |
| 503 | 服务不可用 |
| 连接失败 | 网络错误 |

## 配置步骤（3步，10分钟）

### Step 1：获取 DeepSeek API Key

1. 登录 [DeepSeek 开放平台](https://platform.deepseek.com/api_keys)
2. 创建 API Key（新用户送 500 万 token）
3. 复制保存（只显示一次）

### Step 2：修改 Hermes 配置

编辑 `~/.hermes/config.yaml`：

```yaml
models:
  primary:
    provider: zhipu
    model: glm-5.1

  fallback_model:
    provider: deepseek
    model: deepseek-v4-flash
    api_key: sk-你的DeepSeek密钥
    base_url: https://api.deepseek.com
    api_mode: openai_chat
```

### Step 3：重启生效

```bash
hermes gateway restart
```

## 三个必踩的坑

### 坑1：base_url 不能带后缀

```yaml
# ❌ 错误——会走 Anthropic 协议，导致 400 报错
base_url: https://api.deepseek.com/anthropic

# ✅ 正确——走 OpenAI 兼容协议
base_url: https://api.deepseek.com
```

详见 [[deepseek-protocol-compatibility]] 的完整分析。

### 坑2：api_mode 必须是 openai_chat

```yaml
# ❌ 错误——会尝试用 Anthropic 协议格式发送请求
api_mode: anthropic_messages

# ✅ 正确
api_mode: openai_chat
```

### 坑3：改完配置必须重启

改了配置文件不重启等于没改。

## 成本对比

| 模型 | 输入价格 | 输出价格 | 用途 |
|------|---------|---------|------|
| GLM-5.1 | 免费 | 免费 | 主力模型 |
| DeepSeek V4 Flash | ¥1/百万token | ¥2/百万token | 应急备用 |

## 实测数据（一周运行）

- 主模型限流：约每天 1-2 次，集中在工作日上午
- Fallback 成功率：100%
- 周费用：DeepSeek 不到 ¥0.5
- 用户感知：大部分时候无感切换

## 核心原则

**不要让 AI 服务成为你的单点故障。** 任何依赖单一 API 的工作流，都值得花 10 分钟配一个 fallback。

## 公众号文章

此最佳实践已撰写为公众号教程文章，准备发布到「[[ai-zhiguanju]]」。

## 相关

- [[deepseek-protocol-compatibility]] — DeepSeek 协议兼容性问题的深度分析（三重根因）
- [[hermes-agent]] — Agent 平台，fallback 机制的载体
- [[llm-model-comparison]] — GLM-5.1 vs DeepSeek V4 Pro 对比
- [[wechat-publishing-toolchain]] — 公众号文章发布工具链
