---
title: VS Code Copilot Co-Author 争议
created: 2026-05-04
updated: 2026-05-04
type: concept
tags: [ai-tool, coding, opinion]
sources: [ai-world-digest/2026-05-03]
---

# VS Code Copilot Co-Author 争议

> VS Code 自动在 Git commit 中添加 "Co-Authored-by Copilot"，无论用户是否实际使用了 Copilot。682pts on Hacker News（2026-05-03）。

## 事件

VS Code（GitHub Copilot 扩展）被发现会自动在 Git 提交信息末尾追加 `Co-Authored-by: GitHub Copilot` 标记。关键争议点：

1. **不管是否使用**：即使开发者没有在编写该 commit 的代码时使用 Copilot，也会被加上 Co-Authored-by
2. **默认行为**：这不是用户主动选择的，而是默认开启
3. **归因准确性**：虚假归因违反了 Git commit 的真实性原则

## 引发的讨论

### 归因与透明度

- AI 辅助开发的归因应该由开发者主动声明，而非工具自动添加
- 自动添加虚假归因破坏了 commit history 的可信度
- 对企业合规和代码审计有潜在影响

### 行业趋势

- AI 编程工具越来越积极地在代码中"留名"
- [[llm-wiki-pattern]] 中 Karpathy 提到的 ".md 替代 .sh" 趋势也涉及 AI 与代码的交互方式
- 开发者社区对 AI 工具边界行为的容忍度在降低

## 启示

- AI 工具应尊重开发者的自主权，默认行为应保守
- 归因（attribution）是 AI 伦理的重要议题
- 开源社区对此类行为的监督作用（HN 682pts 说明关注度高）

## 来源

- 2026-05-03 AI世界日报，HN 热门（682pts）

## 相关

- [[ai-world-digest]] — AI 世界日报管线，采集此事件
- [[llm-wiki-pattern]] — AI 与开发者工作流的另一个交叉点
