---
title: Open Design — 开源 AI 设计工具
created: 2026-05-03
updated: 2026-05-04
type: entity
tags: [ai-tool, design, best-practice]
sources: [raw/articles/guangguang-github-april-hot-2026.md]
---

# Open Design (nexu-io/open-design)

> 开源 AI 设计工具，替代 Claude Design，内置71种品牌级设计系统。169pts on Hacker News（2026-05-03）。

## 基本信息

- **GitHub**: https://github.com/nexu-io/open-design
- **Stars**: 11,835（截至2026年5月2日）
- **定位**: 本地优先的开源设计系统
- **语言**: TypeScript

## 核心特性

- **71种品牌级设计系统**内置：Stripe、Linear、Vercel 等
- **多输出格式**：生成网页/桌面/移动原型、幻灯片、图片、视频
- **多 Agent 兼容**：Claude Code、Codex、Cursor、Gemini 等
- **本地优先**：数据不上传，隐私友好

## 对比

| 维度 | Open Design | Claude Design | xinghe-image |
|------|------------|---------------|-------------|
| 开源 | ✅ 完全开源 | ❌ 闭源 | ✅ 开源脚本 |
| 设计系统 | 71种内置 | 有限 | 需手动指定 |
| Agent兼容 | 多Agent | 仅Claude | 仅Hermes |
| 输出类型 | 原型/幻灯片/视频 | 网页原型 | 图片 |

## Dark Theme 技术方案（2026-05-03 实战）

为 SafeTech 安全咨询公司构建暗色主题落地页时总结的设计方法论。

### CSS 变量映射（6变量暗色方案）

```css
:root {
  --bg: #0b0f1a;
  --surface: #131a2e;
  --fg: #e2e8f0;
  --muted: #64748b;
  --border: #1e293b;
  --accent: #3b8bff;       /* 主强调蓝 */
  --accent-secondary: #f97316; /* 次强调橙 */
}
```

将所有颜色收敛到这 6 个 CSS 变量，实现一键切换明暗主题。

### Accent Budget 规则

> 每个强调色（accent color）每屏最多使用 **2次**。超预算则视觉效果混乱。

### Honest Omission 原则

> 没有真实数据就不展示统计数字——宁可跳过 stats section，也不编造虚假指标。

## 质量审查流程

### P0 Checklist（发布前自查）

- ❌ 无裸 hex 色值出现在 `:root` 之外
- ✅ 正确字体加载
- ✅ accent 使用不超过 2次/屏
- ❌ 无紫色渐变
- ❌ 无 emoji 图标

### 五维度评分（5-dim Critique）

| 维度 | 含义 | 最低分 |
|------|------|--------|
| Philosophy | 设计哲学一致性 | ≥4/5 |
| Hierarchy | 视觉层级清晰度 | ≥4/5 |
| Execution | 实现质量 | ≥4/5 |
| Specificity | 行业特异度 | ≥4/5 |
| Restraint | 克制程度（不过度设计） | ≥4/5 |

每个维度必须 ≥4 分才能通过审查。

## 适用场景

- 快速生成品牌级网页原型
- 非设计背景的开发者做 UI
- AI Agent 自动化设计工作流
- 暗色主题落地页快速搭建

## Hermes Skill

- 创建了 `web-prototype` skill，集成 Open Design 到 [[hermes-agent]] 工作流

## 来源

- 2026-05-02 AI世界日报 GitHub 热门项目
- 2026-05-03 SafeTech 落地页实战（ACP sessions 9b02aef0 + f100174e）

## 相关

- [[claude-security]] — 同期 HN 热门开源工具
- [[xinghe-image-skill]] — 图片生成替代方案
- [[hermes-agent]] — 通过 web-prototype skill 集成
- [[remotion]] — 另一个创意内容生成工具
