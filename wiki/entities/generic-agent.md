---
title: GenericAgent
created: 2026-04-26
updated: 2026-05-03
type: entity
tags: [ai-tool, agent, automation, llm]
sources: [raw/articles/guangguang-github-april-hot-2026.md]
---

# GenericAgent

自主进化 AI Agent 框架，让 LLM 长出"双手"——通过 9 个原子工具实现自主任务执行。

## 基本信息

- GitHub: `lsdefine/GenericAgent`（8.4k Stars，2026-05）
- 协议: MIT
- 核心代码量: ~3K 行 Python
- arXiv 论文: `2604.17091`
- 状态: 发布约 3 个月，快速迭代中

## 核心特性

1. **9 个原子工具**: `code_run`, `file_read/write/patch`, `web_scan/execute_js`, `ask_user`, `memory_read/write`
2. **~100 行 Agent Loop**: 极简核心循环
3. **自我进化技能树**: Agent 自动积累和复用技能
4. **MixinSession**: 多模型容错切换，`spring_back` 自动恢复
5. **Token 消耗极低**: <30K 上下文，比同类框架省 10 倍
6. **多端接入**: 微信/QQ/Telegram/飞书/钉钉/企微
7. **自举实证**: 整个仓库从 `git init` 到所有 commit 均由 Agent 自主完成

## 配置要点

### 变量名决定协议（关键设计）

`mykey.py` 中变量命名决定 API 协议：
- 包含 `native_claude` → Anthropic 协议（推荐）
- 包含 `native_oai` → OpenAI 协议
- **必须包含 `native`** 才走原生工具调用，否则走旧的文本解析方式

### 智谱 GLM 端点

| 端点 | URL | 说明 |
|------|-----|------|
| 通用 API | `open.bigmodel.cn/api/paas/v4` | 标准调用 |
| Anthropic 兼容 | `open.bigmodel.cn/api/anthropic` | 推荐，原生工具调用 |
| CodingPlan | `open.bigmodel.cn/api/coding/paas/v4` | 省钱但有封号风险 |

### DeepSeek V4 支持

- Anthropic 兼容端点: `https://api.deepseek.com/anthropic`
- 1M 上下文窗口，384K 最大输出
- `thinking_type: adaptive`

## 踩坑记录

1. **严重数据安全问题**（Issue #28）: Agent 删除操作穿透 Windows junction 导致 D 盘 230+GB 数据误删——**务必在隔离环境使用**
2. **CodingPlan 非官方支持**: GenericAgent 不在智谱 CodingPlan 官方支持列表（仅支持 Claude Code、CodeBuddy、Cursor 等 16 个工具），硬接有封号风险
3. **Python 版本**: 3.14+ 不兼容，必须用 3.13 或更低
4. **API 变量名易搞混**: `oai_claude_config_xxx` 这类命名导致协议匹配错误（已修复但仍需注意）
5. **Skill 调用不稳定**: 重启后可能失效
6. **TMWebDriver 安全漏洞**: 未授权 API 访问

## 与同类框架对比

| 维度 | GenericAgent | [[hermes-agent\|Hermes]] | OpenClaw | Claude Code |
|------|-------------|----------|----------|-------------|
| 代码量 | ~3K 行 | 大型 | ~530K 行 | 大型 |
| Token 消耗 | 极低(<30K) | 中等 | 高(200K-1M) | 中等 |
| 自我进化 | ✅ | ✅ | 插件生态 | ❌ |
| 部署难度 | `pip install` | 多种方式 | 需 8 GPU | `npm install` |
| 数据安全 | ⚠️ 风险较高 | 较安全 | 较安全 | 较安全 |

## 公众号发布实战（2026-04-26 微信端完成）

GenericAgent 教程文章成功发布到「[[ai-zhiguanju]]」草稿箱：
- 原始 HTML 43KB，拆为上下两篇（18.1KB + 20.1KB）
- 上篇（1-6章）：安装、配置、端点选择、MixinSession容错
- 下篇（7-12章）：启动、IM接入、自主行为、排错、配置示例
- 封面图通过 [[xinghe-image-skill]] 8步Turbo模式生成
- Part1 media_id: `K39qDjnxfENs0yskQc4IuLVol5ABQWB0zEqO2yUd5YvmLaiwCyYqXj__sn3hwV4D`
- Part2 media_id: `K39qDjnxfENs0yskQc4IuOTexryr6fR6s-AHPjq4Q6lO4wg6e0fqjZaIpK0s19mO`

## 浏览器控制方式（2026-04-26 CLI调研）

用户调研 GenericAgent 如何控制浏览器进行 Web 自动化。

## 相关

- [[hermes-agent]] — 另一个 AI Agent 平台，生态更完善
- [[wechat-publishing-toolchain]] — 公众号工具链（GenericAgent 支持微信端接入）
- [[hackingtool]] — 另一个安全测试工具合集（185+工具，64.8k stars）

### TMWebDriver 详解

GenericAgent 的浏览器控制方案是 **TMWebDriver**（源码在项目 `/tmp/GenericAgent/` 目录中）：

- **架构**：Chrome 扩展 + Python WebSocket 服务器 + JS 执行双通道
- **核心组件**：TMWebDriver.py（服务器）、simphtml.py（HTML简化）、tmwd_cdp_bridge（扩展）
- **已集成到 [[hermes-agent|Hermes]]**：2026-04-27 完成，设为默认浏览器控制方式
- **优势**：继承用户已登录状态、CSP绕过能力、Token消耗比 Playwright 低 ~4 倍
- **部署位置**：`~/.hermes/tmwebdriver/`

详见 → [[tmwebdriver]]
