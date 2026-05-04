---
title: Hermes Agent
created: 2026-04-22
updated: 2026-05-05
type: entity
tags: [ai-tool, agent, automation]
sources: [raw/articles/linyuebanzi-hermes-llm-wiki-skill-2026.md, raw/articles/keji-jun-hermes-config-guide-2026.md, conversation/2026-04-26, conversation/2026-04-29, conversation/2026-04-30, conversation/2026-05-01, conversation/2026-05-04]
---

# Hermes Agent

Nous Research 开发的 AI Agent 平台。支持多 Agent 协作、内置 skill 系统、浏览器自动化等。

## 与 LLM Wiki 的关系

Nous Research 把 Karpathy 的 LLM Wiki 模式打包成了 Hermes 的内置 skill（llm-wiki），一条命令即可创建和运行知识库，不需要手动配置。

## 核心能力

- 内置 skill 系统（llm-wiki、浏览器控制、代码执行等）
- 多 Agent 协作模式
- 支持 Obsidian 集成
- Web Clipper 支持快速收集素材

## 满配配置（五大模块）

裸装 vs 满配差距巨大，建议按以下顺序配置：

### 1. 身份与记忆
- **SOUL.md**：定义人格和角色，可用 [agency-agents-zh](https://github.com/jnMetaCode/agency-agents-zh) 的 211 个中文角色模板
- **Hindsight**：替代内置 MEMORY，自动提取实体/事实/关系，无容量上限，知识图谱组织 → 详见 [[hindsight-memory]]

### 2. 感知能力（内容抓取）
- **Jina Reader**：单页抓取
- **Crawl4 AI**：批量深度抓取
- **Scrapling**：反爬绕过（官方技能）
- **CamoFox**：隐身浏览器（官方技能）

### 3. 搜索与文档处理
- **Tavily**：AI 搜索（1000次/月免费，主力）
- **DuckDuckGo**：零成本兜底
- **Pandoc**：万能格式转换
- **Marker**：PDF 转 Markdown 增强

### 4. 表达能力
- **Whisper**：语音识别（99+ 语言）
- **Edge TTS**：免费语音合成
- **Fal.ai / FLUX Skill**：图片生成

### 5. Token 精细管控
- **Tokscale**：Token 用量实时监控（`npx tokscale@latest`）
- **hermes-hudui**：按模型/组件/会话拆解成本（localhost:3001）
- **RTK**：压缩终端输出，减少 60-90% Token（`brew install rtk`）
- **hermes-agent-self-evolution**：遗传算法自动优化提示词

## 生态资源

- **awesome-hermes-agent**：一站式资源汇总
- **hermes-ecosystem**：80+ 工具可视化地图
- **wondelai skills**：380 个跨平台 Skill 一次性安装

## Playwright-CLI Skill

已安装在 `~/.hermes/skills/browser/`，提供浏览器自动化能力。

- **持久化 Chrome Profile**：`~/.chrome-automation-profile`，带反检测配置
- **核心优势**：按需返回页面摘要（summary），而非 MCP 方案将整个 DOM 塞入上下文
- **Token 节省**：比传统 MCP 浏览器方案节省约 **4x Token**
- **应用场景**：网站登录态提取（如 [[bilibili-subtitle-extraction]] 的 SESSDATA）、页面数据抓取

## Cron 环境调试技巧

在 Cron（定时任务）环境下调试时有特殊限制：

### 环境变量不可见

- Cron 环境**无法访问** gateway 的环境变量（如 API keys）
- `terminal()` 的 `redact_secrets: true` 会用 `***` 遮蔽所有 secret，无法看到实际值
- **绕过方法**：用 `python3 -c` 内联脚本直接读取配置文件或环境变量：

```bash
python3 -c "import yaml; c=yaml.safe_load(open('/Users/makermz/.hermes/config.yaml')); print(c['api_key'])"
```

### DeepSeek 模型超时

- DeepSeek **50-step 模式**在 Cron 环境下几乎必然超时
- **务必使用 8-step turbo 模式**：`/model` 切换到 `deepseek-v4-flash` 或设置较短 timeout
- Cron 任务 timeout 建议设为 300s（5 分钟）以内

### 调试检查清单

1. 先用 `python3 -c` 内联确认配置值是否正确
2. 确认 `base_url` 和 `api_mode` 匹配（详见 [[deepseek-protocol-compatibility]]）
3. 确认 Cron 环境能访问网络（`ping 8.8.8.8`）
4. 检查 `~/.hermes/logs/` 下的最近日志

## v0.11.0 升级记录（2026-04-30）

### 升级概况

从 v0.10.0 升级到 v0.11.0（上游 tag `v2026.4.23`，领先 1614 commits）。升级过程中遇到 **5 个 merge conflicts**：

| 文件 | 冲突原因 |
|------|---------|
| `agent/anthropic_adapter.py` | DeepSeek `_is_deepseek_anthropic_endpoint` 检测逻辑变更 |
| `gateway/run.py` | `resolve_display_context_length` 实现方式变化 |
| `hermes_cli/models.py` | 模型验证逻辑重构 |
| `run_agent.py` | 配置读取结构变更 |
| `tests/hermes_cli/test_model_validation.py` | 测试用例更新 |

### 上游吸收的变更

以下自定义补丁已被上游集成，无需重新手动应用：

- **DeepSeek `_is_deepseek_anthropic_endpoint` 检测**：上游新增了对 DeepSeek Anthropic 兼容端点的自动识别
- **`reasoning_content` 兼容性**：上游处理了 reasoning_content 字段的兼容逻辑
- **Gateway `resolve_display_context_length`**：上游重构了 context length 的显示解析方式

### 需要重新应用的自定义补丁

上游未集成、需手动恢复的本地定制：

1. **`run_agent.py` — `max_tokens` 配置化**
   - 从 `config.yaml` 的模型配置中读取 `max_tokens`
   - 支持路径：`custom_providers[].models.<id>.max_tokens`

2. **`hermes_cli/models.py` — 自定义 Provider 归一化**
   - `custom:DeepSeek` 格式的 named custom provider 需要归一化处理
   - 确保自定义 provider 名称在 CLI 验证中被正确识别

### 经验教训

- **先 diff 再打补丁**：升级时上游可能已经集成了之前的自定义修改，盲目重新应用会导致重复或冲突。务必先用 `git diff` / `git log` 确认上游已有哪些变更。
- **Cron 环境变量问题（再次确认）**：Cron 会话无法访问 shell profile 中的环境变量，`AISTUDIO_API_KEY` 等需要 `source ~/.zshrc` 或在 config.yaml 中直接配置。详见 [[deepseek-protocol-compatibility]]。
- **`delegate_task` 的中断风险**：delegate task 可以被新用户消息中断，导致所有工作进行丢失。适用于批量工作，不适合作为关键单点任务的依赖。

## Cron `cfg_get` ImportError（2026-05-01）

### 事件

2026年5月1日早6:00，两个 Cron 任务（每日知识库入库 `66ccdc6df1c5` 和 AI世界日报 `efacc6ea4e99`）同时失败。

**错误信息**：
```
Error processing job 66ccdc6df1c5: cannot import name 'cfg_get' from 'hermes_cli.config'
Error processing job efacc6ea4e99: cannot import name 'cfg_get' from 'hermes_cli.config'
```

### 根因

- 4月30日晚上 gateway 重启后，加载的代码版本中 `cfg_get` 函数被移除或重命名
- `hermes_cli/config.py` 中不再包含 `cfg_get` 导出
- 所有依赖该函数的 cron 任务和 chat 会话均受影响

### 解决方案

- **重启 gateway** 后恢复正常（`hermes gateway restart`）
- 重启后加载了修正版本的代码

### 经验教训

- Gateway 重启后应验证 cron 任务是否正常执行（可在重启后手动触发一次）
- 代码升级后如果删除/重命名了导出的函数，需同步更新所有引用方
- 可通过 `~/.hermes/logs/agent.log` 查看详细错误信息定位问题

## 相关

- [[llm-wiki-pattern]] — 内置的核心 skill 之一
- [[obsidian]] — 推荐的 IDE 搭档
- [[hindsight-memory]] — 推荐的记忆升级方案
- [[bilibili-subtitle-extraction]] — Playwright 浏览器自动化的实际应用案例
- [[deepseek-protocol-compatibility]] — DeepSeek 回退模型协议兼容性
- [[ai-world-digest]] — Hermes Cron 任务案例

## 记忆方案调研（2026-05-04）

调研了 [[mempalace]] 作为可选的增强记忆方案：

- **当前方案**：[[hindsight-memory]]（Hermes 内置）+ session_search → 覆盖日常场景
- **MemPalace 优势**：全量逐字存储、语义搜索 R@5 96.6%、MCP 集成（29 个工具）、多 AI 工具共享记忆
- **结论**：暂时收藏备用，待记忆需求超出 Hindsight 能力时再考虑切换

## 安全生产工具链（2026-05-04）

开发了 [[hseffyun-spider]]（ABC 安全文件爬虫），基于 Playwright-CLI 批量采集 hseffyun.com 文档。标志着 Hermes 工具链从 AI/技术领域扩展到安全生产领域。

