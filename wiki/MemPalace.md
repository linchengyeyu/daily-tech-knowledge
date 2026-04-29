# MemPalace

> 本地优先的开源AI记忆系统，5万⭐，MIT协议

- GitHub: https://github.com/MemPalace/mempalace
- 官网: https://mempalaceofficial.com/
- 语言: Python 3.9+
- 协议: MIT
- 创建: 2026-04-05

## 核心理念

逐字存储对话/文件，不做摘要不做改写，用语义搜索检索。

宫殿式结构：人/项目→翼(wing)，话题→房间(room)，内容→抽屉(drawer)。

## 技术要点

- 默认ChromaDB向量存储，后端可插拔
- 内置知识图谱(SQLite)
- 支持MCP(29个工具)，可接Claude Code/Gemini CLI等
- LongMemEval R@5 96.6%(纯语义搜索)，混合策略98.4%
- ~300MB磁盘(嵌入模型)，无需API key

## 快速上手

```bash
pip install mempalace
mempalace init ~/projects/myapp
mempalace mine ~/projects/myapp                    # 导入项目文件
mempalace mine ~/.claude/projects/ --mode convos   # 导入Claude对话
mempalace search "关键词"                           # 语义搜索
mempalace wake-up                                  # 加载上下文
```

## 适用场景

- 多AI工具共享记忆(Claude Code/Gemini/Cursor)
- 对话量大需全量回溯
- 精确检索某次对话原始内容

## 备注

Hermes自带memory + session_search已能覆盖日常场景。MemPalace适合更重度的记忆需求，暂时收藏备用。
