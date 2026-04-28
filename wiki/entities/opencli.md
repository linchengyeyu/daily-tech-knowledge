---
title: OpenCLI
created: 2026-04-29
updated: 2026-04-29
type: entity
tags: [ai-tool, automation, coding]
sources: [conversation/2026-04-28]
---

# OpenCLI

通用 CLI Hub 工具，90+ 网站适配器（B站/知乎/小红书/Twitter 等），复用 Chrome 浏览器登录态，零 LLM 消耗。

## 基本信息

| 项目 | 值 |
|------|-----|
| GitHub | `jackwener/opencli` (17.8k⭐) |
| 版本 | v1.7.8 |
| Chrome 扩展 | v1.0.2 (Web Store ID: `ildkmabpimmkaediidaifkhjpohdnifk`) |
| Daemon 端口 | `19825`（默认） |
| 安装命令 | `npm install -g @jackwener/opencli` |
| 环境要求 | Node.js >= 21 |

## 安装步骤

1. 全局安装：`npm install -g @jackwener/opencli`
2. 运行 `opencli doctor` 验证 daemon 运行
3. 安装 Chrome 扩展（从 GitHub releases 下载或 Chrome Web Store）
4. 在 `chrome://extensions/` 加载扩展（Developer Mode → Load unpacked）
5. 重新运行 `opencli doctor` 确认连通性

## Bilibili 适配器

最常用适配器，命令示例：

```bash
opencli bilibili me          # 个人信息
opencli bilibili hot         # 热门内容
opencli bilibili comments    # 评论
opencli bilibili search      # 搜索
opencli bilibili subtitle    # 字幕提取
opencli bilibili favorite    # 收藏夹
opencli bilibili feed        # 关注动态
opencli bilibili history     # 浏览历史
```

## 与 TMWebDriver 对比

| 维度 | OpenCLI | [[tmwebdriver]] |
|------|---------|-----------------|
| 适用范围 | 90+ 预定义站点 | 任意网页 |
| 输出格式 | 结构化 JSON | 原始 DOM 文本 |
| LLM 消耗 | 零 | 低 |
| 扩展性 | 适配器开发 | 任意 JS 执行 |
| 适合场景 | 常见站点快速操作 | 复杂页面交互 |

## 踩坑

- Daemon 正常但 extension not connected → 需手动在 Chrome 加载扩展
- 扩展路径：`/Volumes/DevSSD/Applications/opencli/opencli-extension/`
- 配置持久化在 `~/.opencli/sites/<site>/`

## 相关

- [[tmwebdriver]] — 替代浏览器控制方案
- [[bilibili-subtitle-extraction]] — B站字幕提取
- [[hermes-agent]] — 已集成 OpenCLI skill
