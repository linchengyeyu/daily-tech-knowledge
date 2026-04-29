# Hermes 这个技能我一直没碰，跑完一遍后悔没早试

来源：微信公众号「林月半子的AI笔记」
作者：林月半子
发布时间：2026年4月17日
URL: https://mp.weixin.qq.com/s/q6Q-0-9_sOjt29NTTPQO0g

---

## 核心概念

Karpathy 的 LLM Wiki 模式，被 Nous Research 打包成 Hermes Agent 的内置 skill（llm-wiki）。

一句话比喻：**Obsidian 是你的 IDE，LLM 是你的程序员，Wiki 就是你的代码库。**

## 解决的痛点

传统 RAG（ChatGPT/NotebookLM）每次提问都从原始文档临时检索拼接，像金鱼7秒记忆，知识从不沉淀。
LLM Wiki 的做法是先"编译"——把原始材料消化成结构化 Wiki 页面网络，后续查询都在编译好的 Wiki 上进行。

## 三层骨架设计

### 第一层：raw（原始来源层）
原始材料（文档、文章、笔记、代码）。铁律：LLM 只读不改。

### 第二层：wiki（编译层）
LLM 根据 SCHEMA 规则编译出来的页面网络：
- entities/ — 实体页（工具、人、项目）
- concepts/ — 概念页
- comparisons/ — 对比页
- queries/ — 查询回填页
- index.md — 总目录
- log.md — 操作日志
靠 [[wikilink]] 双向互联。

### 第三层：SCHEMA（规则层）
SCHEMA.md 文件，规定 Wiki 的结构、命名、处理规则，人和 AI 共同维护。

## 实操四步

1. **初始化**：`/llm-wiki 创建一个用于XXX的知识库` → 自动搭好目录
2. **投喂素材**：丢链接或用 Obsidian Web Clipper 积累，然后 `ingest raw/ 里的所有素材`
3. **提问**：基于编译好的 Wiki 回答，高质量回答自动归档到 queries/
4. **定期 lint**：`lint 这个 wiki` → 检查矛盾、过时内容、孤儿页、缺失索引

## 关键提醒

- raw 层放什么比工具选什么重要——放自己的东西才是"你的思想地图"
- 红绿灯原则：
  - 绿灯区（放心交给LLM）：摘要、索引更新、链接补全、格式调整、孤儿页检查
  - 黄灯区（一起审）：矛盾裁决、概念合并、过时内容作废
  - 红灯区（绝对自己来）：核心事实写入、价值判断、最终签字
- 个人量级（100篇/40万字）不需要向量数据库
- 先窄后宽，先跑通一类素材再扩展
