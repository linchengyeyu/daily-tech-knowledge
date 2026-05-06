---
title: DeepClaude
created: 2026-05-05
updated: 2026-05-07
type: entity
tags: [ai-tool, llm, agent, coding]
sources: [ai-world-digest/2026-05-04, conversation/2026-05-06]
---

# DeepClaude

开源项目，将 DeepSeek V4 Pro 与 Claude Code Agent 结合，通过 Agent 循环大幅降低 AI 编程成本（约降低17倍）。

## 基本信息

| 项目 | 值 |
|------|-----|
| GitHub | [aattaran/deepclaude](https://github.com/aattaran/deepclaude) |
| Stars | 1329 ⭐ |
| 协议 | MIT |
| 定位 | 低成本 AI 编程 Agent 方案 |
| 核心模型 | DeepSeek V4 Pro（推理） + Claude Code（Agent框架） |
| 成本降幅 | ~17倍（vs 直接使用 Claude） |
| HN 热度 | 142 pts |
| 日期 | 2026-05-04 HN 热榜 |

## 核心原理

通过环境变量重定向 API 请求实现低成本替换：
- `ANTHROPIC_BASE_URL` 改为 DeepSeek 端点 `https://api.deepseek.com/anthropic`
- 无需 Anthropic 账户，只需 DeepSeek API Key
- DeepSeek V4 Pro 作为推理引擎，替代昂贵的 Claude/GPT 模型
- 利用 Claude Code 的 Agent 循环能力进行任务编排
- 适合预算有限但需要 Agent 级编程能力的开发者

## 本地部署记录（2026-05-06）

| 项目 | 详情 |
|------|------|
| 安装路径 | `/Volumes/DevSSD/Applications/deepclaude/` |
| CLI路径 | `/usr/local/bin/deepclaude` |
| API Key | 配置在 `~/.zshrc`（DEEPSEEK_API_KEY） |
| 安装状态 | ✅ 成功 |

### 使用方式

```bash
deepclaude  # 直接运行，使用 DeepSeek V4 Pro 替代 Claude
```

### 已知问题

| Bug | 详情 | 状态 |
|-----|------|------|
| Issue #3 | 请求没走 DeepSeek 仍用 Claude token | 需先执行 `claude logout` |
| 不支持图片 | 无法处理视觉输入 | 限制 |
| MCP 不兼容 | MCP 工具协议无法使用 | 限制 |
| benchmark 报错 | macOS 上 `date` 不支持 `%3N` | 兼容性 bug |

## 相关

- [[deepseek-protocol-compatibility]] — DeepSeek API 协议兼容性问题
- [[deepseek-fallback-best-practice]] — DeepSeek Fallback 配置最佳实践
- [[hermes-agent]] — 同样使用 Agent 循环模式的 AI 平台
- [[llm-model-comparison]] — GLM-5.1 vs DeepSeek-V4-Pro 对比
