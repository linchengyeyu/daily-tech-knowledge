---
title: 星河AI生图Skill
created: 2026-04-24
updated: 2026-04-24
type: entity
tags: [ai-tool, agent, automation]
sources: []
---

# 星河AI生图Skill（xinghe-image）

基于百度飞桨 ERNIE-Image-Turbo 的 AI 生图工具，适用于[[wechat-publishing-toolchain|公众号]]配图。

## 基本信息

| 项目 | 详情 |
|------|------|
| GitHub | liuyunlin/xinghe-image |
| 安装路径 | ~/.hermes/skills/creative/xinghe-image/ |
| 模型 | ernie-image-turbo（⚠️必须全小写） |
| API | 百度AIStudio，OpenAI兼容格式 |
| API端点 | https://aistudio.baidu.com/llm/lmapi/v3 |
| Key获取 | https://aistudio.baidu.com/account/accessToken |
| 环境变量 | AISTUDIO_API_KEY |
| 依赖 | Python 3.8+ + openai库 |

## 四种场景

| 场景 | 默认尺寸 | 比例 | 风格路线 |
|------|---------|------|---------|
| 📰 封面图/Banner | 1376x768 | 16:9 | 组装路线(styles-index.csv) |
| 🖼️ 文章配图 | 1264x848 | 3:2 | 组装路线(styles-index.csv) |
| 📊 信息图 | 1264x848 | 3:2 | 预设路线(image-presets.csv) |
| 📱 小红书图文 | 848x1264 | 3:4 | 预设路线(image-presets.csv) |

## 支持的7种尺寸

`1024x1024` `848x1264` `768x1376` `896x1200` `1264x848` `1376x768` `1200x896`

## 风格体系

### 组装路线（46种风格）
按mood分类：
- 未来/科技(5): 科技萌趣3D、复古未来主义、赛博朋克、原始美学、复古未来女性
- 极简/安静(4): 博物馆核、手绘线稿、安静图形极简、Notion扁平插画
- 强烈/冲击(3): 新粗野主义、强对比字体海报
- 实验/前卫(3): 反设计风、拼凑字体、变异复古
- 复古/怀旧(3): 孔版印刷、复古现代主义、复古照排字
- 做旧/质感(3): 噪点风、精致颗粒、复印机美学
- 几何/结构(4): 工程标注、几何图案、模块图形、微观图形学
- 手工/温暖(7): 反AI手作、触感暖调、有机自然、刺绣、机械植物、黏土动画、太阳朋克
- 叙事/插画(3): 故事标签、在地文化、叙事字体海报
- 拼贴/混媒(4): 杂志拼贴、数字剪贴簿、混合媒介×2
- 优雅/轻奢(2): 轻奢极简、高反差衬线
- 活力/多巴胺(3): 多巴胺高饱和、最大化主义、动感排字

### 预设路线（30条预设）
覆盖：学科知识卡片、清单可视化、商业插画等，直接可用。

## 调用命令

```bash
# 基础生图
python3 ~/.hermes/skills/creative/xinghe-image/scripts/generate.py \
  --prompt "提示词（中文效果更好）" \
  --size 1376x768 \
  --output output.png

# 高质量（50步）
python3 ~/.hermes/skills/creative/xinghe-image/scripts/generate.py \
  --prompt "提示词" --size 1376x768 --output out.png \
  --steps 50 --no-pe

# 公众号封面
python3 ~/.hermes/skills/creative/xinghe-image/scripts/generate.py \
  --prompt "一张科技感的AI主题封面图..." --size 1376x768 --output cover.png

# 文章配图
python3 ~/.hermes/skills/creative/xinghe-image/scripts/generate.py \
  --prompt "一张展示AI编程的插画..." --size 1264x848 --output illust.png
```

## 中文渲染约束

提示词含中文时，末尾自动追加：
```
所有中文文字清晰可辨，笔画完整，无乱码、无变形、无错位；中文字符独立排版，字体工整易读。图中所有文字必须使用中文，不得出现日文、韩文或其他语言文字。
```

## 视觉一致性技巧

API不支持 `--ref` 参数。保持系列一致性的方式：
- 第2张起完整复用第1张的风格描述
- 末尾追加：`风格、色调、渲染质感与系列第一张图保持高度一致。`

## 参考文件

| 文件 | 用途 |
|------|------|
| references/styles-index.csv | 46种风格库 |
| references/image-presets.csv | 30条预设提示词 |
| references/workflows/prompt-assembly.md | 风格推荐+组装规则 |
| references/workflows/cover-image.md | 封面图子流程 |
| references/workflows/article-illustration.md | 文章配图子流程 |
| references/workflows/infographic.md | 信息图子流程 |
| references/workflows/xiaohongshu.md | 小红书图文子流程 |
