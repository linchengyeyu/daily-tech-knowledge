---
title: B站字幕提取工具调研
created: 2026-04-27
updated: 2026-05-05
type: entity
tags: [ai-tool, automation, coding]
sources: [conversation/2026-04-26, conversation/2026-05-04]
---

# B站字幕提取工具调研

调研 Bilibili 视频字幕/CC 字幕的提取方案，核心结论：**需要登录态（SESSDATA）才能获取 AI 生成的字幕**。

## 工具推荐 Top 4

| 工具 | ⭐ Stars | 特点 |
|------|---------|------|
| Bilibili-Evolved | 29k | 浏览器油猴脚本，功能最全 |
| BBDown | 13.8k | 命令行下载器，支持字幕 |
| bilibili-api | 3.9k | Python SDK，适合编程集成 |
| yutto | 1.8k | 命令行批量下载 |

## bilibili-api Python SDK (v9.1.0)

### 安装踩坑

- **PyYAML 5.4.1 编译失败**：需先 `pip install PyYAML==6.0.3` 再装 bilibili-api
- Python 环境：系统 Python 3.9
- pip user install path：`/Users/makermz/Library/Python/3.9/lib/python/site-packages/`
- 已安装包：`bilibili-api==9.1.0`, `aiohttp==3.13.5`, `requests==2.32.5`

### 关键发现

1. **不登录只返回空字幕列表**——AI 生成字幕需要 SESSDATA cookie
2. 字幕 API 端点：`/x/player/wbi/v2?bvid=...&cid=...`
3. SESSDATA 有效期约 **30 天**

### SESSDATA 提取方法

利用 [[hermes-agent]] 的 playwright-cli skill（`~/.hermes/skills/browser/`），通过 Playwright persistent profile 自动从登录后的 B 站提取 SESSDATA：

- 持久化 Chrome profile：`~/.chrome-automation-profile`
- 凭证文件存储：`~/.bilibili-credentials.json`

### 测试结果

- 测试视频：**BV16poGBLEbZ**
- 成功返回 **1386 条多语言字幕**
- 验证了完整的字幕提取流程可行

## 深度调研（2026-05-04）

### 调研范围

对 B 站字幕/弹幕获取工具进行全面调研，覆盖 GitHub、npm、PyPI，共梳理 **30+ 项目**，按功能分为五大类。

### CC 字幕获取 Top 推荐

| 优先级 | 项目 | ⭐ Stars | 核心优势 |
|--------|------|---------|---------|
| 🥇 1 | bilibili-subtitle（哔哔君） | 1,123 | 浏览器扩展，一键查看/下载/翻译/总结 CC 字幕 |
| 🥈 2 | bilibili-api（Python库） | 3,862 | API 调用，`video.get_subtitle()`，适合编程集成 |
| 🥉 3 | yutto | 1,814 | CLI 批量下载视频+CC 字幕+弹幕 ASS |
| 4 | Bilibili-Evolved | 29,091 | 功能最全的增强脚本，含字幕下载模块 |
| 5 | BBDown | 13,769 | 专业下载器，`--sub-only` 只下载字幕 |

### 工具分类

| 分类 | 数量 | 代表项目 |
|------|------|---------|
| 重点推荐（CC字幕） | 7 | Bilibili-Evolved, bilibili-subtitle, yutto, BBDown, bilibili-api, bilix |
| CC字幕专用工具 | 10 | bilibili-subtitle-tweaks, bccdc 等 |
| MCP 服务器（AI Agent集成） | 4 | bilibili-mcp-server(184⭐), bilibili-mcp-js(165⭐) |
| 弹幕专用工具 | 8 | pakku.js(2.6k⭐), danmaku2ass(613⭐) |
| PyPI/npm 包 | 4 | bilibili-api, bilix, yutto, biliass |

### CC 字幕 API 说明

1. **获取字幕列表**：`https://api.bilibili.com/x/player/wbi/v2?bvid=xxx&cid=xxx`（需 WBI 签名）
2. **字幕格式**：BCC JSON → `{"body": [{"from": 0.0, "to": 5.0, "content": "字幕文本"}]}`
3. **字幕来源**：UP 主上传 / B 站 AI 自动生成（`ai_status` 字段标识）

### 针对 AI Agent 集成的推荐

| 优先级 | 项目 | 理由 |
|--------|------|------|
| 1 | bilibili-mcp（adoresever） | MCP Server，支持搜索/评论/字幕/弹幕/回复 |
| 2 | bilibili-subtitle-fetcher-skill | 直接输出 Markdown，适合知识整理 |
| 3 | bilibili-subtitle-download-skill | AI Agent Skill，适合 Agent 工作流 |

## 相关

- [[hermes-agent]] — Playwright 浏览器自动化能力，用于 SESSDATA 提取
- [[xinghe-image-skill]] — 同属 AI 工具生态，国内可用的免费 AI 生图方案
- [[wechat-publishing-toolchain]] — 字幕内容可用于公众号文章素材
