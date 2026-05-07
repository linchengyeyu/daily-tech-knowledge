---
title: SOUL.md AI Agent人格定义
created: 2026-05-08
updated: 2026-05-08
type: entity
tags: [ai-tool, agent, best-practice]
sources: [conversation/2026-05-07]
related: [hermes-agent, wechat-content-strategy, mercury-agent, agent-soul-architecture]
---

# SOUL.md AI Agent人格定义

Tony Simons (@tonysimons_) 发表的文章「The 170-Line SOUL.md That Made My Hermes Agent Dangerous」（630赞、1911收藏）提出的 AI Agent 人格定义方法论。

## 核心理念

不给 AI 当"helpful assistant"，而是通过 markdown 文件定义：身份、反对规则、双向问责、自主权边界、项目地图。

**关键转变**：从"AI当你的助手"到"你定义AI的灵魂"。

## SOUL.md 结构

一份完整的 SOUL.md 包含以下模块：

### 1. 身份定义
- Agent 是谁、做什么、不为谁服务
- 明确的边界和角色定位

### 2. 性格基调
- 说话风格、态度、价值观倾向
- 非泛泛的"专业友好"，而是有具体人格特征

### 3. 反对义务（Duty to Object）
- Agent 不仅要执行，还有权反对用户的错误方向
- 类似"伦理刹车"，但更实用——技术方向反对也算

### 4. 反向约束（管住用户）
- 对用户的约束规则
- 4件事需批准才可执行：
  1. **发布** — 任何对外发布操作
  2. **花钱** — 涉及费用支出
  3. **不可逆操作** — 删除、覆盖等
  4. **改 SOUL.md** — 修改自身定义文件

### 5. 项目地图
- 当前在做什么、各项目的优先级和状态
- Agent 据此理解上下文

### 6. 输出标准
- 质量要求、格式规范、交付标准

### 7. 问责循环
- 定期回顾、自我评估、改进机制

## 实际应用

小王已基于此框架创建了 `/Users/makermz/.hermes/SOUL.md`（4607字节），定制了适合个人工作流的 Agent 人格定义。

## 相关概念

- 这个概念与 [[mercury-agent]] 的 soul.md 是同源思路，详见抽象分析 [[agent-soul-architecture]]
- 在 [[wechat-content-strategy]] 的内容运营中，SOUL.md 的"反对义务"理念可用于内容质量把控

## 相关

- [[hermes-agent]] — 已配置 SOUL.md 的 Agent 平台
- [[mercury-agent]] — 另一个 soul-driven Agent 实现
- [[agent-soul-architecture]] — 从 SOUL.md 和 Mercury 抽象出的共同架构概念
- [[wechat-content-strategy]] — 内容运营方法论
