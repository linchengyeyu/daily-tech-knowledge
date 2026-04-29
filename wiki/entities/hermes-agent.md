---
title: Hermes Agent
created: 2026-04-22
updated: 2026-04-30
type: entity
tags: [ai-tool, agent, automation]
sources: [raw/articles/linyuebanzi-hermes-llm-wiki-skill-2026.md, raw/articles/keji-jun-hermes-config-guide-2026.md, conversation/2026-04-26, conversation/2026-04-29]
---

# Hermes Agent

Nous Research 开发的 AI Agent 平台。支持多 Agent 协作、内置 skill 系统、浏览器自动化等。

## 与 LLM Wiki 的关系

Nous Research 把 Karpathy 的 LLM Wiki 模式打包成了 Hermes 的内置 skill（llm-wiki），一条命令即可创建和运行知识库，不需要手动配置。

## 核心能力

- 内置 skill 系统（llm-wiki、浏览器控制、代码执行等）
- 多 Agent 协作模式
- 支持 Obsidian 集成
- Web Clipper 支持快速收集素材

## 满配配置（五大模块）

裸装 vs 满配差距巨大，建议按以下顺序配置：

### 1. 身份与记忆
- **SOUL.md**：定义人格和角色，可用 [agency-agents-zh](https://github.com/jnMetaCode/agency-agents-zh) 的 211 个中文角色模板
- **Hindsight**：替代内置 MEMORY，自动提取实体/事实/关系，无容量上限，知识图谱组织 → 详见 [[hindsight-memory]]

### 2. 感知能力（内容抓取）
- **Jina Reader**：单页抓取
- **Crawl4 AI**：批量深度抓取
- **Scrapling**：反爬绕过（官方技能）
- **CamoFox**：隐身浏览器（官方技能）

### 3. 搜索与文档处理
- **Tavily**：AI 搜索（1000次/月免费，主力）
- **DuckDuckGo**：零成本兜底
- **Pandoc**：万能格式转换
- **Marker**：PDF 转 Markdown 增强

### 4. 表达能力
- **Whisper**：语音识别（99+ 语言）
- **Edge TTS**：免费语音合成
- **Fal.ai / FLUX Skill**：图片生成

### 5. Token 精细管控
- **Tokscale**：Token 用量实时监控（`npx tokscale@latest`）
- **hermes-hudui**：按模型/组件/会话拆解成本（localhost:3001）
- **RTK**：压缩终端输出，减少 60-90% Token（`brew install rtk`）
- **hermes-agent-self-evolution**：遗传算法自动优化提示词

## 生态资源

- **awesome-hermes-agent**：一站式资源汇总
- **hermes-ecosystem**：80+ 工具可视化地图
- **wondelai skills**：380 个跨平台 Skill 一次性安装

## Playwright-CLI Skill

已安装在 `~/.hermes/skills/browser/`，提供浏览器自动化能力。

- **持久化 Chrome Profile**：`~/.chrome-automation-profile`，带反检测配置
- **核心优势**：按需返回页面摘要（summary），而非 MCP 方案将整个 DOM 塞入上下文
- **Token 节省**：比传统 MCP 浏览器方案节省约 **4x Token**
- **应用场景**：网站登录态提取（如 [[bilibili-subtitle-extraction]] 的 SESSDATA）、页面数据抓取

## Cron 环境调试技巧

在 Cron（定时任务）环境下调试时有特殊限制：

### 环境变量不可见

- Cron 环境**无法访问** gateway 的环境变量（如 API keys）
- `terminal()` 的 `redact_secrets: true` 会用 `***` 遮蔽所有 secret，无法看到实际值
- **绕过方法**：用 `python3 -c` 内联脚本直接读取配置文件或环境变量：

```bash
python3 -c "import yaml; c=yaml.safe_load(open('/Users/makermz/.hermes/config.yaml')); print(c['api_key'])"
```

### DeepSeek 模型超时

- DeepSeek **50-step 模式**在 Cron 环境下几乎必然超时
- **务必使用 8-step turbo 模式**：`/model` 切换到 `deepseek-v4-flash` 或设置较短 timeout
- Cron 任务 timeout 建议设为 300s（5 分钟）以内

### 调试检查清单

1. 先用 `python3 -c` 内联确认配置值是否正确
2. 确认 `base_url` 和 `api_mode` 匹配（详见 [[deepseek-protocol-compatibility]]）
3. 确认 Cron 环境能访问网络（`ping 8.8.8.8`）
4. 检查 `~/.hermes/logs/` 下的最近日志

## 相关

- [[llm-wiki-pattern]] — 内置的核心 skill 之一
- [[obsidian]] — 推荐的 IDE 搭档
- [[hindsight-memory]] — 推荐的记忆升级方案
- [[bilibili-subtitle-extraction]] — Playwright 浏览器自动化的实际应用案例
- [[deepseek-protocol-compatibility]] — DeepSeek 回退模型协议兼容性
- [[ai-world-digest]] — Hermes Cron 任务案例
