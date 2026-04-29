# Wiki Schema

## Domain
通用个人知识库——覆盖安全生产、AI工具、基金理财、技术学习、项目文档、读书笔记等。

## Conventions
- 文件名：小写英文+连字符，不用空格和中文（如 `safety-production-law.md`）
- 每个 Wiki 页面开头必须有 YAML frontmatter（见下方模板）
- 页面之间用 `[[wikilinks]]` 双向链接（每页至少2个出站链接）
- 更新页面时必须刷新 `updated` 日期
- 新页面必须加到 `index.md` 对应分类下
- 每次操作必须追加到 `log.md`

## Frontmatter
```yaml
---
title: 页面标题
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: entity | concept | comparison | query | summary
tags: [从下方标签库选取]
sources: [raw/articles/source-name.md]
---
```

## Tag Taxonomy

### 安全生产
safety-law, safety-standard, hidden-danger, safety-insurance, safety-report, accident-case

### AI & 技术
ai-tool, llm, prompt-engineering, agent, automation, deployment, coding, model-benchmark

### 投资 & 理财
fund, stock, investment-strategy, market-analysis

### 项目 & 产品
project-doc, product-design, business-model, user-growth

### 通用
person, company, book, course, tutorial, comparison, best-practice, opinion, glossary

规则：只能用上面的标签。需要新标签时先加到这里再用。

## Page Thresholds
- **创建页面**：实体/概念在 2+ 来源中出现，或在一篇来源中是核心主题
- **更新已有页面**：来源提到了已有页面的新信息
- **不创建页面**：顺带一提的名字、跟领域无关的细节
- **拆分页面**：超过 200 行时拆成子主题，互相链接
- **归档页面**：内容完全过时时移入 `_archive/`，从 index 移除

## Entity Pages
每人/组织/产品/工具一个页面。包含：
- 概述
- 关键事实和日期
- 与其他实体的关系（`[[wikilinks]]`）
- 来源引用

## Concept Pages
每个概念/主题一个页面。包含：
- 定义/解释
- 当前知识状态
- 未解决的问题或争论
- 相关概念（`[[wikilinks]]`）

## Comparison Pages
对比分析页面。包含：
- 对比什么、为什么对比
- 对比维度（优先用表格）
- 结论或综合判断
- 来源

## Update Policy
新信息与已有内容冲突时：
1. 比较日期——新的来源通常覆盖旧的
2. 如果确实矛盾，同时记录两个观点，标注日期和来源
3. 在 frontmatter 标记：`contradictions: [page-name]`
4. 在下次 lint 时标记给用户审核
