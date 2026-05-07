---
title: Mercury Agent
created: 2026-05-08
updated: 2026-05-08
type: entity
tags: [ai-tool, agent, comparison]
sources: [conversation/2026-05-07]
related: [hermes-agent, soul-md, agent-soul-architecture]
---

# Mercury Agent

GitHub: [cosmicstack-labs/mercury-agent](https://github.com/cosmicstack-labs/mercury-agent)
npm 包：`@cosmicstack/mercury-agent`

## 概述

Soul-driven AI Agent，人格通过用户拥有的 markdown 文件定义。定位为轻量级 Telegram+CLI 个人助手。

## 人格定义系统（多文件分离）

Mercury 使用多个独立的 markdown 文件定义 Agent 人格：

| 文件 | 职责 |
|------|------|
| `soul.md` | 核心灵魂定义 |
| `persona.md` | 人格特征、说话风格 |
| `taste.md` | 审美偏好、选择倾向 |
| `heartbeat.md` | 定期行为、检查节奏 |

与 [[soul-md]]（Hermes 的单文件方案）不同，Mercury 将人格拆分为多个关注点分离的文件。详见 [[agent-soul-architecture]]。

## "Second Brain" 记忆系统

Mercury 的核心竞争力在于结构化记忆系统：

### 10种结构化类型

1. **identity** — 身份信息
2. **preference** — 用户偏好
3. **goal** — 目标设定
4. **project** — 项目信息
5. **habit** — 习惯模式
6. **decision** — 决策记录
7. **constraint** — 约束条件
8. **relationship** — 人际关系
9. **episode** — 事件记录
10. **reflection** — 反思总结

### 技术实现

- **存储**：SQLite + FTS5 全文搜索
- **自动冲突解决和合并**：多来源记忆可自动合并
- **结构化查询**：按类型、时间、关联度检索

## 与 Hermes 对比

| 维度 | Mercury Agent | [[hermes-agent]] |
|------|--------------|-----------------|
| 定位 | 轻量个人助手 | 全功能 Agent 平台 |
| 平台覆盖 | Telegram + CLI | 20+ 平台（微信、飞书、CLI等） |
| 人格定义 | 多文件分离（4个md） | 单文件 SOUL.md |
| 记忆系统 | 结构化（10类型，SQLite+FTS5） | 扁平文本，手动管理 |
| 权限控制 | 精细（文件级别） | 较粗（基于 SOUL.md 声明） |
| 多 Agent | 不支持 | 支持 |
| 浏览器自动化 | 无 | Playwright-CLI |
| MCP | 不支持 | 支持 |
| 优势 | 结构化记忆强、权限控制精细 | 平台覆盖广、多agent、浏览器自动化 |

### Hermes 记忆系统局限（对比 Mercury 时暴露）

- **扁平文本**：MEMORY.md 是纯文本，无结构化分类
- **手动管理**：需人工维护和清理
- **字符限制**：当前 98% 使用率（2157/2200 字符），接近上限

## 相关

- [[hermes-agent]] — 主要对比对象
- [[soul-md]] — Soul-driven Agent 的另一种实现
- [[agent-soul-architecture]] — 从两个项目中抽象出的共同架构概念
- [[mempalace]] — 另一个结构化 AI 记忆系统（5万⭐）
