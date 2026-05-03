---
title: PPT Master — AI 生成可编辑 PPT
created: 2026-05-03
updated: 2026-05-04
type: entity
tags: [ai-tool, automation, deployment]
sources: [raw/articles/guangguang-github-april-hot-2026.md]
---

# PPT Master

AI 生成真正的原生 PPTX 文件的工具（hugohe3/ppt-master，10.7k⭐）。每个形状、文本框、图表都是独立可编辑对象，在 PowerPoint 里想怎么改就怎么改。

## 输入格式

PDF、Word、URL、Markdown 文档

## 特性

- 自定义模板支持
- 内置 22 个示例项目，共 309 页
- 多种风格：杂志风、学术风、暗黑艺术风、自然纪录片风、科技 SaaS 等
- **v2.5.0 新增**：音频旁白 + 视频导出（edge-tts + ffmpeg）

## 生成管线（Pipeline）

```
Source → Project Init → Template → Strategist（八项确认，BLOCKING）→ Image Acquisition → Executor（顺序 SVG 生成）→ Post-processing → Export PPTX
```

1. **Strategist 阶段**：八项确认（BLOCKING），必须全部通过才继续
2. **Image Acquisition**：获取图片素材
3. **Executor**：顺序生成 SVG 文件
4. **Post-processing** → **Export**：生成最终 PPTX

> **用户需求**：希望使用 Xinghe/百度 API 生成写实照片级图片，而非 SVG 矢量图。参考 [[xinghe-image-skill]]。

## 环境搭建记录（2026-05-03）

### pycairo 构建修复

安装依赖时 `pycairo` 构建失败。**解决方法**：通过 Homebrew 安装 `pkgconf`：

```bash
brew install pkgconf
```

> cairo 本身已安装，缺的是 `pkgconf`（替代 pkg-config），安装后 pycairo 编译通过。

### UV 虚拟环境

- 使用 UV 创建虚拟环境，Python 3.13
- 路径：`/Volumes/DevSSD/project/ppt-master/.venv/bin/python3`

### 核心依赖

| 包 | 版本 | 用途 |
|---|---|---|
| python-pptx | 1.0.2 | PPTX 文件生成 |
| pymupdf | — | PDF 处理 |
| svglib | — | SVG 解析 |
| edge-tts | — | TTS 音频旁白 |
| reportlab | 4.5.0 | PDF/图形渲染 |
| flask | — | Web 界面 |

### Hermes Skill 创建

创建了 `ppt-master` skill（productivity 类别），用于在 [[hermes-agent]] 中直接调用 PPT Master。

## 链接

- GitHub: https://github.com/hugohe3/ppt-master
- 来源：[[逛逛GitHub 4月热门开源项目]]

## 相关

- [[remotion]] — React 代码做视频动画，不同方向的创意内容生成工具
- [[xinghe-image-skill]] — 百度 ERNIE-Image 生图，可作为 PPT Master 图片源
- [[hermes-agent]] — 通过 skill 集成 PPT Master
