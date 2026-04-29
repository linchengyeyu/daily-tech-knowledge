---
title: Remotion 视频动画框架
created: 2026-04-27
updated: 2026-04-27
type: entity
tags: [ai-tool, coding, automation]
sources: [conversation/2026-04-26]
---

# Remotion 视频动画框架

用 React 代码制作视频动画的框架，适合程序员以编程方式生成视频内容。

## 环境信息

- **Node.js**: v25.9.0
- **项目路径**: `/Volumes/DevSSD/project/my-remotion/`
- **Studio 端口**: 35511

## 安装踩坑记录

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| `create-video` 交互式选择器无法非交互操作 | CLI 不支持 `--yes` 模式 | 手动创建项目结构 |
| `.ts` 文件不支持 JSX | TypeScript 配置未开启 JSX | 改用 `.tsx` 扩展名 |
| 版本不匹配 (4.0.0 vs 4.0.451) | 初始化模板版本过旧 | 升级到最新版 |

## LoserCard 倒霉蛋卡片动画

为「百万进度条」基金视频系列制作的卡片翻转动画。

### V1
基础卡片翻转效果。

### V2 特效清单
- 浮动红色粒子
- 问号脉冲发光
- 白屏闪光
- 红色冲击波
- 屏幕震动
- **-1.82% 砸落动画**
- 印章效果

## 渲染

- 透明背景渲染：**ProRes 4444**
- 渲染命令：
  ```bash
  npx remotion render src/index.tsx LoserCard out/loser-card-v2.mp4
  ```

## 应用场景

- 百万进度条基金视频系列——用代码生成投资亏损的动画效果
- 参考视频：芝士Dreamer 的 AI 视频动画制作流程（BV1eedSBBEre）

## 相关

- [[ai-zhiguanju]] — 公众号内容创作可能需要视频素材
- [[bilibili-subtitle-extraction]] — 从 B 站参考视频提取字幕用于学习
