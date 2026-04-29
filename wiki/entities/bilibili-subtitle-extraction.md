---
title: B站字幕提取工具调研
created: 2026-04-27
updated: 2026-04-27
type: entity
tags: [ai-tool, automation, coding]
sources: [conversation/2026-04-26]
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

## 相关

- [[hermes-agent]] — Playwright 浏览器自动化能力，用于 SESSDATA 提取
- [[xinghe-image-skill]] — 同属 AI 工具生态，国内可用的免费 AI 生图方案
