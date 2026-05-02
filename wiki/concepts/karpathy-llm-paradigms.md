---
tags: [llm, karpathy, ai-paradigm, insights]
related: [karpathy, llm-wiki-pattern]
last_updated: 2026-05-03
---

# Karpathy 的 LLM 三大新范式

> Andrej Karpathy 在红杉 Ascent 大会（2026年5月）上分享的 LLM 发展三大新范式。

## 三大范式

### 1. 菜单生成应用被 LLM 完全吞噬

传统"菜单驱动"的软件应用正在被 LLM 的自然语言交互完全替代。用户不再需要从菜单选择功能，直接描述需求即可。

### 2. 用 .md 技能替代 .sh 脚本

传统运维/自动化依赖 shell 脚本（.sh），未来将转向 Markdown 格式的"技能"文件（.md）。LLM 可以直接理解并执行 Markdown 描述的任务流程，比 shell 脚本更直观、更可维护。

- 与 Hermes Agent 的 Skill 系统（SKILL.md）理念完全一致
- 降低自动化门槛，非程序员也能编写和维护自动化流程

### 3. 非结构化知识库计算

LLM 使非结构化知识库（如 Markdown 文件、Wiki）变得"可计算"。不再需要事先定义 schema、建表、写 SQL，直接用自然语言查询和推理。

- Karpathy 的 LLM Wiki 项目是这一理念的实践
- 本 wiki（Obsidian + Hermes）也是这一范式的体现

## LLM "锯齿状能力"现象

Karpathy 解释了为什么 LLM 在某些任务上表现出色，但在看似简单的事情上却失败：**经济因素决定了训练数据分布**。

- 模型能力不均匀，是因为训练数据分布不均匀
- 被广泛讨论/写过的领域（编程、写作）→ 数据丰富 → 能力强
- 冷门领域 → 数据稀少 → 能力弱
- 这不是技术缺陷，而是经济现实

## 与现有实践的关联

| Karpathy 范式 | 我们的实践 |
|--------------|-----------|
| .md 技能替代 .sh | Hermes Skill 系统（SKILL.md） |
| 非结构化知识库计算 | Obsidian Wiki + session_search |
| 菜单应用被吞噬 | 公众号/飞书 Bot 自然语言交互 |

## 来源

- 2026-05-02 AI世界日报（Karpathy 推特 @karpathy，红杉 Ascent 大会分享）
