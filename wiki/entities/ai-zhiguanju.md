---
title: AI智管局
created: 2026-04-24
updated: 2026-05-05
type: entity
tags:
  - project-doc
  - product-design
  - ai-tool
  - user-growth
sources: [conversation/2026-05-04]
---

# AI智管局

微信公众号，专注AI入门教程和技术科普。

## 基本信息

| 项目 | 详情 |
|------|------|
| 公众号名 | AI智管局 |
| AppID | wxa62b217b2ea99768 |
| 目标读者 | AI入门小白 |
| 内容方向 | AI工具教程、技术科普 |
| 关联B站 | 百万进度条（UID: 252071912）|

## ⚠️ 品牌名注意

- 公众号是「AI智管局」，不是「百万进度条」
- 百万进度条是B站名，别搞混
- 文章落款/引导关注区一律用AI智管局

## 写作要求

- 内容要详细，面向刚入门AI的小白
- 代码块要好看（技术文章核心需求）
- 图片必须要有（公众号算法对有图文章加权，流量更好）

## 工具链

详见 [[wechat-publishing-toolchain]]

### 核心Skills
- [[wechat-publisher]] — 发布到草稿箱
- [[xinghe-image-skill]] — AI生成配图
- wechat-article-formatter — bm.md排版渲染

### 配图服务对比
详见 [[wechat-image-generation-comparison]]

## 品牌定位升级（2026-05-04）

### 「AI工具质检局」—— 不泛泛介绍AI工具，而是实测 + 对比 + 避坑

市场上AI工具宣传多但质量参差不齐，AI智管局定位为"AI质检员"，提供实测数据和客观评价。

### 全平台矩阵

详见 [[multi-platform-content-strategy]]：

| 平台 | 形式 | 自动化程度 |
|------|------|-----------|
| 公众号 | 深度长文 | 全自动上传草稿 |
| 抖音 | 竖版短视频30-60s | [[opencli]] 可发 |
| 小红书 | 图文6-9张卡片 | [[opencli]] 可发 |
| 知乎 | 回答+专栏 | [[opencli]] 可发 |
| B站 | 竖版短视频 | 需手动 |
| 快手 | 竖版短视频 | 需手动 |

### 视频制作

- 使用 [[remotion]] 程序化生成竖版短视频（TTS配音+字幕+动画）
- 四种视频模板：对比横评、踩坑实录、清单推荐、实测教程

### 一周涨粉100人计划

- 方案文件：`/Users/makermz/.hermes/workspace/ai-zhiguanju-growth-plan.md`
- 目标：一周内涨粉100人（微信封闭生态中极度困难）
- 发布节奏：Agent写好→上传草稿箱→用户每天下午4-6点审核发布
- 7篇选题覆盖：AI横评、免费工具、AI做PPT、AI视频对比、Agent评测、数据对比、年度红黑榜
