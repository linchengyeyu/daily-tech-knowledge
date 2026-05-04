---
title: ABC安全文件爬虫
created: 2026-05-05
updated: 2026-05-05
type: entity
tags: [safety-law, automation, coding]
sources: [conversation/2026-05-04]
---

# ABC安全文件爬虫

基于 [[hermes-agent]] Playwright-CLI 的安全文件批量爬取脚本，从 hseffyun.com 按日期范围采集 ABC 安全文档。

## 基本信息

| 项目 | 值 |
|------|-----|
| 脚本路径 | `~/hseffyun_spider.py` |
| 目标站点 | `http://www.hseffyun.com/app-abchse/` |
| 依赖 | playwright-cli（Hermes Skill） |
| 语言 | Python 3 |
| 创建日期 | 2026-05-04 |

## 功能

1. 按日期范围（如 `20260101-20260401`）逐日爬取文档列表
2. 筛选下载人数超过阈值（默认20）的热门文档
3. 输出每行一个网页地址到 txt 文件
4. 支持去重（同一文档在多个日期出现时保留下载量最高的记录）

## 使用方法

```bash
# 基本用法
python3 hseffyun_spider.py 20260101-20260401

# 自定义阈值和输出
python3 hseffyun_spider.py 20260101-20260131 -t 30 -o ./output.txt
```

### 参数

| 参数 | 说明 | 默认值 |
|------|------|--------|
| 日期范围 | 格式：`起始日期-结束日期`，如 `20260101-20260401` | 必填 |
| `-t` | 下载人数最低阈值 | 20 |
| `-o` | 输出 txt 文件路径 | `./hseffyun_docs_{起始}_{结束}.txt` |

## 技术实现

### 采集原理

1. 打开 Playwright 浏览器实例
2. 对每个日期构造 URL：`documentlist.html?indexWord={日期}`
3. 通过 `page.route()` 拦截 API 响应（`/dapi/ccode/run*get_documents*`）
4. 点击「加载更多」按钮直到全部加载（最多20次）
5. 从拦截的响应中提取文档 uuid、文件名、下载人数
6. 关闭浏览器

### 输出格式

每行一个文档详情页 URL：
```
http://www.hseffyun.com/app-abchse/documentdetail.html?document_uuid={uuid}
```

## 安全生产应用

此脚本用于批量发现 hseffyun.com 上的热门安全文档，辅助安全生产知识收集。与 Wiki 的安全生产标签域（`safety-law`, `safety-standard` 等）配合使用。

## 相关

- [[hermes-agent]] — Playwright-CLI 浏览器自动化能力，本脚本的运行依赖
- [[wechat-publishing-toolchain]] — 安全文档内容可用于公众号文章素材
