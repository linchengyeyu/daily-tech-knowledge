---
title: LLM Wiki 模式
created: 2026-04-22
updated: 2026-04-22
type: concept
tags: [ai-tool, automation, best-practice]
sources: [raw/articles/linyuebanzi-hermes-llm-wiki-skill-2026.md]
---

# LLM Wiki 模式

Karpathy 提出的一种知识管理方法：让 LLM 把原始材料"编译"成结构化的 Wiki 页面网络，而不是每次查询都从原文临时检索（传统 RAG 的做法）。

## 核心比喻

> Obsidian 是你的 IDE，LLM 是你的程序员，Wiki 就是你的代码库。

代码库越写越厚、结构越来越清晰，不用每次都从空白文件夹重新来。

## vs 传统 RAG

| 维度 | 传统 RAG | LLM Wiki |
|------|---------|----------|
| 查询方式 | 每次从原文临时检索拼接 | 在编译好的 Wiki 上查询 |
| 知识沉淀 | 无，每次独立 | 有，持续积累 |
| 一致性 | 同一问题可能不同答案 | 编译后保持一致 |
| 跨文档关联 | 弱 | 强，[[wikilinks]] 双向互联 |
| 使用越久 | 体验不变 | 越用越好（知识复利）|

## 三层架构

1. **raw（原始来源层）**：文档、文章、笔记。LLM 只读不改。
2. **wiki（编译层）**：LLM 自动生成的实体页/概念页/对比页，靠 [[wikilinks]] 互联。
3. **SCHEMA（规则层）**：SCHEMA.md 定义结构和规则，人+AI 共同维护。

## 关键操作

- **Ingest**：投喂新素材 → 自动编译出多个 Wiki 页面，更新 index 和 log
- **Query**：基于编译好的 Wiki 回答问题，好答案归档到 queries/
- **Lint**：定期检查矛盾论点、过时内容、孤儿页、缺失索引（建议每周一次）

## 红绿灯原则（审核策略）

- 🟢 **绿灯**（放心交给LLM）：摘要、索引、链接补全、格式调整
- 🟡 **黄灯**（一起审）：矛盾裁决、概念合并、过时内容
- 🔴 **红灯**（自己来）：核心事实写入、价值判断

## 适用规模

个人量级（~100篇/40万字）不需要向量数据库，靠 index.md + 摘要够用。

## 相关

- [[hermes-agent]] — 内置了 llm-wiki skill
- [[obsidian]] — 最佳 IDE 搭档
- [[karpathy]] — 原始思路提出者
