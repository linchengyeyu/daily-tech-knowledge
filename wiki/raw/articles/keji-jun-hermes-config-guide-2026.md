# 装完 Hermes 一定要配置这五套系统，秒变满配版

- 来源：微信公众号「编译硅基」（作者：科技君，@congge918）
- 原文链接：https://mp.weixin.qq.com/s/-1CQxvdc1bDMrPzIHFPpbA
- 发布日期：2026-04-23

---

裸装 Hermes 和满配 Hermes 完全是两种工具——前者是普通的 AI 对话助手，后者才是真正强大的 AI Agent。满配版能力：长期记忆系统、全网信息抓取、语音+图片生成、Token 消耗更少。

## Hermes 五大配置模块

- **身份与记忆**：告诉它你是谁
- **感知能力**：让它读懂互联网
- **表达能力**：让它能说能画
- **效率和成本**：精细管控 Token
- **生态导航**：一站式资源入口

## 第一步：编写 SOUL.md 定义人格和角色

使用 agency-agents-zh 库，里面有 211 个中文角色模板。

GitHub 地址：https://github.com/jnMetaCode/agency-agents-zh

包含 46 个中国市场原创智能体（覆盖小红书、抖音、微信、飞书、钉钉、B 站、跨境电商、政务 ToG、医疗合规等垂直领域）。

角色按部门分类（工程、设计、营销、产品、游戏、安全、金融、HR 等 18 个部门），每个角色都是独立的 .md 文件，包含完整的人设、专业流程和可交付成果。

## 第二步：把内置的 MEMORY.md 换成 Hindsight

| 维度 | 内置 MEMORY | Hindsight |
|------|------------|-----------|
| 写入机制 | 只有 Hermes 认为重要时才写入 | 自动从每轮对话提取实体、事实、关系、时间戳 |
| 容量上限 | ≈ 2200 字符（硬上限） | 无硬上限 |
| 知识组织 | 线性文本 | 知识图谱 |

操作步骤：
1. `hermes memory setup`
2. 选择 `hindsight`
3. 获取 API Key：https://ui.hindsight.vectorize.io/connect
4. 验证：`hermes memory status`

## 第三步：安装内容抓取工具

- **Jina Reader**：单页抓取
- **Crawl4 AI**：批量深度抓取
- **Scrapling**：反爬绕过
- **CamoFox**：隐身浏览器

CamoFox 和 Scrapling 是官方原生/可选技能，通过 `hermes tools + pip` 启用。

## 第四步：安装搜索与文档处理工具

- **Tavily**：AI 专用搜索，1000 次/月免费
- **DuckDuckGo**：零成本兜底搜索
- **Pandoc**：万能格式转换器
- **Marker**：PDF 转 Markdown 增强

搜索能力：Tavily（主力）+ DuckDuckGo（兜底）

## 第五步：安装表达能力工具链

- **Whisper**：语音识别，99+ 语言
- **Edge TTS**：语音合成，免费
- **Fal.ai**：图片生成
- **FLUX Skill**：高质量出图

## 第六步：Token 精细管控

### Tokscale
CLI 监控工具，实时查看全局 Token/成本（TUI 可视化 + JSON 导出）。
```
npx tokscale@latest
# 或 bunx tokscale@latest
```
命令：`tokscale`、`tokscale --hermes`、`tokscale --hermes --week`、`tokscale --json`、`tokscale models`

### hermes-hudui
按模型/组件/会话深度拆解 Token 成本、实时 WebSocket 更新。
```
git clone https://github.com/joeynyc/hermes-hudui.git
cd hermes-hudui && ./install.sh
hermes-hudui  # 访问 http://localhost:3001
```

### RTK（Rust Token Killer）
Rust 零依赖 CLI 代理，智能过滤/压缩终端输出，减少 60-90% Token。
```
brew install rtk
# 或 curl -fsSL https://raw.githubusercontent.com/rtk-ai/rtk/refs/heads/master/install.sh | sh
rtk init -g  # 集成到 Hermes
```

### Hermes-agent-self-evolution
遗传算法自动优化 Agent 提示词和行为（DSPy + GEPA 遗传-帕累托进化算法）。
```
git clone https://github.com/NousResearch/hermes-agent-self-evolution.git
cd hermes-agent-self-evolution && pip install -e ".[dev]"
```

### Skill 扩展
一次性装 wondelai 的 380 个跨平台 Skill。

## 第七步：Hermes 生态入口

- **awesome-hermes-agent**：一站式资源汇总
- **hermes-ecosystem**：80+ 工具可视化地图
