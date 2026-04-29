---
title: AI配图服务对比
created: 2026-04-24
updated: 2026-04-24
type: comparison
tags: [ai-tool, comparison, best-practice]
sources: []
---

# AI配图服务对比

对比适用于[[wechat-publishing-toolchain|公众号配图]]的免费AI生图方案。

## 结论

**选择 xinghe-image（百度ERNIE-Image）** 作为主力方案，Pollinations.ai 作为备用。

理由：中文渲染强、免费、国内直连、无需翻墙、46种专业风格覆盖公众号场景。

## 方案对比

### 方案一：Pollinations.ai

| 维度 | 详情 |
|------|------|
| 网址 | https://pollinations.ai |
| GitHub | pollinations/pollinations (4.4k⭐) |
| 费用 | 免费起步，Pollen积分制 |
| 注册 | GitHub账号 |
| 翻墙 | 需要 |
| 模型 | FLUX Schnell, GPT Image, Z-Image等 |
| 调用 | `GET https://image.pollinations.ai/prompt/{描述}?width=900&height=500` |
| 速度 | 2-5秒 |

**优点：**
- 旧API无需注册、无需Key，curl直接用
- FLUX模型质量好，99.3%成功率
- 开源项目，社区活跃

**缺点：**
- 已开始Pollen积分制，免费额度Spore层约10张/小时
- 旧API随时可能废弃
- 中文生图效果差，必须英文提示词
- 部分高端模型(Grok/NanoBanana Pro)已PAID
- Beta阶段定价可能变
- 需翻墙

### 方案二：xinghe-image（百度ERNIE-Image）

| 维度 | 详情 |
|------|------|
| 网址 | https://github.com/liuyunlin/xinghe-image |
| GitHub | liuyunlin/xinghe-image (0⭐，极新) |
| 费用 | 完全免费（百度AIStudio） |
| 注册 | 百度账号 |
| 翻墙 | 不需要 |
| 模型 | ERNIE-Image-Turbo (8B, Apache 2.0) |
| 调用 | Python脚本，OpenAI兼容格式 |
| 速度 | 3-5秒(Turbo) |

**优点：**
- 完全免费，登录百度账号即拿Key
- 中文渲染能力强（ERNIE-Image核心优势）
- 46种专业风格 + 30条预设提示词
- 国内直连，不翻墙
- 封面图1376x768正好16:9适合公众号
- 模型开源可自部署

**缺点：**
- 项目极新（发布<2天），未经大量验证
- ERNIE-Image 8B质量不如DALL-E 3/Midjourney
- 免费额度具体上限不透明
- 不支持图生图
- 系列图视觉一致性不够稳定

### 其他免费/低价方案

| 服务 | 费用 | 特点 |
|------|------|------|
| SiliconFlow硅基流动 | Kolors模型免费 | 国内、OpenAI兼容 |
| HuggingFace Inference | 免费额度（有限） | 模型最多 |
| Together AI | 新用户$5免费额度 | FLUX系列顶级模型 |
| Replicate | flux-schnell $0.003/图 | 极低价 |
| Novita AI | $0.001/图 | 最便宜的付费选项 |

## MCP Server方案

| 项目 | ⭐ | 免费？ | 说明 |
|------|-----|--------|------|
| MCPollinations | 41 | ✅ | Pollinations的MCP封装 |
| fal-mcp-server | 43 | 有免费tier | Fal.ai生图MCP |

## 公众号配图专用Skills

| 项目 | ⭐ | 功能 |
|------|-----|------|
| Tech-Article-Illustration-Master | 19 | 25种设计风格，反AI塑料感，输出提示词 |
| xinghe-image | 0 | 直接生图，46风格+30预设，国内免费 |
| Generative-Media-Skills | 3.1k | 最成熟多模态Skill，图片+视频+音频 |
| qiaomu-mondo-poster-design | 724 | 大师级海报/封面，支持公众号 |
