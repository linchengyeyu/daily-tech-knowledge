---
title: 微信公众号写作工具链
created: 2026-04-24
updated: 2026-05-01
type: concept
tags: [ai-tool, automation, agent, best-practice]
sources: []
---

# 微信公众号写作工具链

公众号「[[ai-zhiguanju]]」的 AI 辅助写作工具链，基于 Hermes Agent 的 skill 体系构建。

## 当前架构

公众号名：**AI智管局**（AppID: wxa62b217b2ea99768）
目标读者：AI入门小白
内容方向：AI工具教程、技术科普

### 已安装的 Skills

| Skill | 路径 | 功能 |
|-------|------|------|
| wechat-publisher | social-media/wechat-publisher | 官方API直连：图片上传→排版→推送草稿箱 |
| wechat-article-formatter | social-media/wechat-article-formatter | bm.md 渲染Markdown为公众号HTML，代码块/表格/引用样式好看 |
| wechat-article-publisher2 | social-media/wechat-article-publisher2 | 第三方平台(wx.limyai.com)API发布，备用 |
| xinghe-image | creative/xinghe-image | 百度ERNIE-Image生图，封面图/配图/信息图，46种风格 |

## 工作流

```
1. 内容/素材输入
2. xinghe-image 生成配图（封面图 + 章节配图）
3. wechat-article-formatter 渲染Markdown为排版HTML（代码块高亮）
4. wechat-publisher 上传图片到微信素材库 + 推送草稿箱
5. 用户在公众号后台预览发布
```

## 排版规范

### 全局规则
- 所有样式内联，禁止 `<style>` 标签和 CSS class
- 正文宽度 677px
- 字体：-apple-system, PingFang SC, Microsoft YaHei
- 正文字号 15px，行高 1.8

### 两种排版方案

**方案A：wechat-publisher 内置排版**
- 手动内联CSS，适合精细控制
- 主色调 #1e90ff（道奇蓝）
- 引导关注区渐变蓝色背景

**方案B：wechat-article-formatter（bm.md渲染）**
- 调用 bm.md API 渲染，代码块效果好
- 接口：`POST https://bm.md/api/markdown/render`
- 参数：`markdownStyle=green-simple`, `codeTheme=kimbie-light`
- CSS主色调已改为蓝色 #1e90ff
- 代码块：深色背景(#282c34)、Consolas等宽字体
- 表格：斑马纹交替背景
- 引用块：蓝色左边框

### 文章结构模板
```
1. 关注引导文字
2. 封面图
3. 分隔线
4. 摘要引导块（蓝色左边框）
5. 正文各章节（二级标题+段落+配图+代码块）
6. 渐变分割线
7. 引导关注区（渐变蓝色，关注+回复关键词获取资料）
8. END + 公众号名称落款「AI智管局」
```

## 配图方案

详见 [[xinghe-image-skill]]

### 快速调用
```bash
# 封面图（16:9）
python3 ~/.hermes/skills/creative/xinghe-image/scripts/generate.py \
  --prompt "提示词" --size 1376x768 --output cover.png

# 文章配图（3:2）
python3 ~/.hermes/skills/creative/xinghe-image/scripts/generate.py \
  --prompt "提示词" --size 1264x848 --output illust.png
```

## 配图服务对比

详见 [[wechat-image-generation-comparison]]

## 实战经验（2026-04-24 发布 MacBook Pro 文章）

### bm.md API 踩坑
- 返回 JSON 键名是 `"result"` 不是 `"html"`
- Python urllib 会被 403 拒绝，必须用 `curl` 调用
- 大 payload 必须写文件再用 `curl -d @file`，避免 shell 转义问题
- curl 输出含控制字符，先保存到文件再用 `json.load()` 读取

### 发布流程验证
1. 上传封面图 → `material/add_material?type=image` → 获取 `media_id`
2. 渲染 Markdown → bm.md API → 获取 HTML
3. 推送草稿 → `draft/add` → 获取 `media_id`
4. ✅ 首次成功发布：MacBook Pro 自动熄屏教程

### 封面图生成
- 首次运行时 `AISTUDIO_API_KEY` 未配置，用 PIL 生成占位图
- 后续已配置星河 API Key，可直接生成

## 常见错误

| 错误码 | 含义 | 解决 |
|--------|------|------|
| 40007 | invalid media_id | 先上传封面图获取 thumb_media_id |
| 40164 | IP not in whitelist | 以微信报错中的IP为准，加到公众号IP白名单 |
| 45003 | title too long | 标题不超过32个汉字 |

## 长文章拆分策略（2026-04-26 实战经验）

当文章 HTML 超过 ~30KB 时，模型在排版+图片URL替换步骤容易上下文溢出，导致反复返回空响应甚至触发 fallback 链路崩溃。

### 拆分规则
- 单篇 HTML 控制在 **15-25KB** 以内（约 3000-5000 字纯文本）
- 拆分点选在**章节边界**，保持每篇内容完整独立
- 标题格式：「xxx（上）：前半部分主题」「xxx（下）：后半部分主题」
- 每篇独立生成封面图、独立上传、独立发草稿
- 上篇末尾加"下篇预告"引导区块，下篇开头加"本文为下篇"引导

### 已验证安全范围
- 单篇 18-20KB HTML 可稳定完成排版+上传全流程
- 实例：GenericAgent 教程（原始 HTML 43KB）拆为 18.1KB + 20.1KB 两篇，均成功

### 导致溢出的完整故障链
1. HTML 过长 → 模型上下文溢出
2. 返回空响应 → 触发 3 次重试
3. 切换到 deepseek-v4-pro fallback
4. fallback 遇到 thinking mode 兼容性错误（API 要求 thinking 内容回传）
5. 全链路失败

## 文章写作要求（用户反馈 2026-04-26）

读者看到文章时不明白发生了什么，需要：
1. **背景铺垫**：每个知识点先交代"为什么做这件事"
2. **故事线叙述**：按时间或逻辑顺序，像讲故事一样串联
3. **问题→解决过程→结论**：三段式结构
4. **关键细节不省略**：报错信息、配置项名称、命令参数
5. **口语化但不随意**：像跟同事分享经验，信息密度要高

## 注意事项

- ⚠️ 公众号名是「AI智管局」，不是「百万进度条」（百万进度条是B站名）
- 草稿必须传封面图，否则报40007
- 微信API报的出口IP和curl查到的可能不一样，以微信报错为准
- IP白名单修改后即时生效
- bm.md 返回值用 `data["result"]` 不是 `data["html"]`
- 复杂 JSON payload 不要用 `node -e` 内联，写到文件再执行
- deepseek-v4-pro 的 thinking mode API 不兼容：要求 `thinking` 内容回传，当前架构未处理
- 50步生图模式不稳定（60/90/120s超时均失败），统一用8步Turbo模式

## 文章质量评分（2026-04-30验证）

> 详细标准见 [[wechat-article-scoring]]

使用 DeepSeek API 对文章按八维度自动打分，总分 ≥ 90（A级）才允许上传草稿箱。

首次自动化评分实测（2026-04-30）：文章得分 **88/100**，距 A 级差 2 分，主要扣分在「互动引导」和「标题与封面」两个维度。修改后重新评分达标再发布。

## bm.md 流程图上传经验

流程图/图表（Mermaid 等）不能直接在 Markdown 中内联交给 bm.md 渲染——微信不支持外部 JS/CDN。

**正确做法：**
1. 先将流程图/图表渲染为静态图片（本地 Mermaid CLI 或在线工具）
2. 通过微信 `media/uploadimg` API 将图片上传到公众号素材库，获取微信返回的图片 URL
3. 将该 URL 以 `![描述](微信图片URL)` 的形式嵌入 Markdown 中
4. 再将包含微信图片 URL 的 Markdown 交给 bm.md 渲染

这样 bm.md 渲染出的 HTML 中，图片已经是微信域名的 URL，在公众号内可正常显示。
