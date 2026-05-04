---
title: Archon — AI 编码工作流引擎
created: 2026-05-03
updated: 2026-05-03
type: entity
tags: [ai-tool, coding, agent, automation]
sources: [raw/articles/guangguang-github-april-hot-2026.md]
---

# Archon

AI 编码工作流引擎，把开发流程编码成确定性 YAML 工作流，解决 AI Coding 结果不确定的问题。

## 核心理念

Dockerfile 规范基础设施，GitHub Actions 规范 CI/CD → AI 编码流程也需要规范。

## 特性

- YAML 工作流定义：确定性步骤（测试、脚本）+ AI 智能环节混合编排
- 独立 git worktree 执行，5 个修复任务可并行互不冲突
- 内置 17 个默认工作流：修 issue、想法→PR、代码审查、安全重构
- Web UI 可视化拖拽编辑
- 支持 Slack、Telegram、Discord、GitHub 远程触发

## 技术演进

从 Python 迁移到 TypeScript，定位从 AI Agent 构建器转型为 AI 编码工作流引擎。

## 链接

- GitHub: https://github.com/coleam00/Archon
- 来源：[[逛逛GitHub 4月热门开源项目]]

## 相关

- [[rtk]] — 另一个优化 AI Coding 体验的工具（省 token）
- [[matt-pocock-skills]] — Claude Code Skills 合集
