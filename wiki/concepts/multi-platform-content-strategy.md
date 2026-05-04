---
title: 全平台内容运营策略
created: 2026-05-05
updated: 2026-05-05
type: concept
tags: [user-growth, automation, best-practice]
sources: [conversation/2026-05-04]
---

# 全平台内容运营策略

从 [[ai-zhiguanju]] 一周涨粉100人计划中提炼的全平台内容分发方法论。

## 核心理念

**一条内容 → 六种形态**：写一篇深度文章，衍生出公众号长文、抖音短视频、小红书图文卡片、知乎回答、B站视频、快手视频。

## 品牌定位：「AI工具质检局」

不做泛泛的AI工具介绍，而是**实测 + 对比 + 避坑**。市场上宣传多但质量参差不齐，需要"AI质检员"角色。

## 六平台矩阵

| 平台 | 内容形式 | 自动化工具 | 用户操作 |
|------|---------|-----------|---------|
| 公众号 | 深度长文 | wechat-publisher 全自动上传草稿 | 审核后发布 |
| 抖音 | 竖版短视频30-60s | [[opencli]] douyin draft/publish | 需注册新号 |
| 小红书 | 图文6-9张卡片 | [[opencli]] xiaohongshu publish | 需注册新号 |
| 知乎 | 回答+专栏 | [[opencli]] zhihu answer/search | 需注册新号 |
| B站 | 竖版短视频 | 需手动上传 | 切到AI智管局号 |
| 快手 | 竖版短视频 | 手动 | 需注册新号 |

## 视频制作方案

- 使用 [[remotion]] 程序化生成竖版短视频（TTS配音+字幕+动画）
- 四种模板：对比横评、踩坑实录、清单推荐、实测教程
- [[xinghe-image-skill]] 生成小红书图文卡片

## 一周选题示例

1. DeepSeek vs ChatGPT vs Kimi写周报谁最强？
2. 别交智商税！这5个AI工具完全免费
3. 我用AI做PPT，老板以为我熬夜了
4. Sora vs 可灵 vs Vidu，AI视频谁最能打？
5. Manus是真Agent还是套壳？72小时深度体验
6. AI写公众号 vs 人写公众号，7天数据对比
7. 2026年AI工具红黑榜

## 关键洞察

- Agent 持续运行 + 人类协作是未来10年主流工作模式（Dan Shipper）
- AI 不会取代工程师反而会创造更多岗位（Aaron Levie）
- 微信封闭生态中涨粉极度困难，需靠多平台引流

## 相关

- [[ai-zhiguanju]] — 公众号主体
- [[opencli]] — 多平台自动化发布工具
- [[remotion]] — 视频制作框架
- [[wechat-publishing-toolchain]] — 公众号发布工具链
- [[wechat-article-scoring]] — 文章质量评分体系
