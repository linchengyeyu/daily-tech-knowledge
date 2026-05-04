---
title: RTK — Rust 写的省 Token 神器
created: 2026-05-03
updated: 2026-05-03
type: entity
tags: [ai-tool, coding, automation]
sources: [raw/articles/guangguang-github-april-hot-2026.md]
---

# RTK

Rust 写的 CLI 代理工具，专门为 AI Coding 工具（[[claude-code]]、Cursor、Codex 等）节省 token。

## 核心问题

AI Coding 工具执行 git status、npm test 等命令时，所有输出都塞进上下文窗口。一次 git status ≈ 2000 token，跑测试上万。冗余输出挤占推理空间，上下文过早溢出，API 费用涨。

## 解决方案

- 拦截并压缩命令输出，平均压缩率 80-90%
- Hook 机制自动改写命令（git status → rtk git status），对 AI 透明
- 单个二进制文件，零依赖，开销 < 10ms

## 支持范围

- 100+ 种命令智能过滤：git、测试框架、构建工具、Docker、AWS
- 12 种 AI 工具：[[hermes-agent|Claude Code]]、Cursor、Gemini CLI、Codex 等

## 链接

- GitHub: https://github.com/rtk-ai/rtk
- 来源：[[逛逛GitHub 4月热门开源项目]]

## 相关

- [[claude-mem]] — Claude Code 记忆插件，另一种节省上下文的方案
- [[GenericAgent]] — 同样关注 token 效率的 Agent 框架
