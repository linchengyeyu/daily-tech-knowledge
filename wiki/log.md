# Wiki Log

> 所有操作按时间顺序记录。只追加不修改。
> 格式：`## [YYYY-MM-DD] action | subject`
> 操作类型：ingest, update, query, lint, create, archive, delete
> 超过 500 条时轮转：改名为 log-YYYY.md，重新开始。

## [2026-04-22] create | Wiki initialized
- Domain: 通用个人知识库（安全生产、AI工具、基金理财、技术学习、项目文档）
- Structure created with SCHEMA.md, index.md, log.md
- 9 subdirectories created under raw/, entities/, concepts/, comparisons/, queries/

## [2026-04-22] ingest | 林月半子「Hermes 这个技能我一直没碰，跑完一遍后悔没早试」
- Raw source: raw/articles/linyuebanzi-hermes-llm-wiki-skill-2026.md
- Created pages:
  - concepts/llm-wiki-pattern.md（LLM Wiki 模式核心概念）
  - entities/hermes-agent.md（Hermes Agent 工具介绍）
  - entities/obsidian.md（Obsidian 笔记工具）
  - entities/karpathy.md（Andrej Karpathy 人物）
- Updated: index.md（新增4条目）, log.md（本条记录）

## [2026-04-23] ingest | 无辣的学习笔记「Cloudflare Tunnel 内网穿透方案」
- Raw source: raw/articles/wula-cloudflare-tunnel-2026.md
- Created pages:
  - concepts/cloudflare-tunnel.md（CF Tunnel 原理、部署、加速方案）
  - entities/qnap-nas.md（QNAP NAS 设备信息）
- Updated: index.md（新增2条目，Total pages: 6）

## [2026-04-23] ingest | 编译硅基「装完 Hermes 一定要配置这五套系统」
- Raw source: raw/articles/keji-jun-hermes-config-guide-2026.md
- Created pages:
  - concepts/hindsight-memory.md（Hindsight 长期记忆方案）
- Updated pages:
  - entities/hermes-agent.md（新增满配五大模块配置：身份记忆/感知/搜索/表达/Token管控）
- Updated: index.md（新增1条目，Total pages: 7）

## [2026-04-24] create | 微信公众号写作工具链调研
- 新增页面：
  - entities/ai-zhiguanju.md（AI智管局公众号基本信息、品牌名注意、写作要求）
  - entities/xinghe-image-skill.md（星河AI生图Skill完整文档，46种风格+调用命令）
  - concepts/wechat-publishing-toolchain.md（公众号写作工具链：排版规范、工作流、已安装Skills）
  - comparisons/wechat-image-generation-comparison.md（免费AI配图服务对比：Pollinations vs xinghe-image）
- 背景：为公众号「AI智管局」建立写作工具链
  - 安装了 wechat-article-formatter（bm.md排版渲染，代码块高亮）
  - 安装了 wechat-article-publisher2（第三方API发布备用）
  - 安装了 xinghe-image（百度ERNIE-Image生图，免费国内可用）
  - 选择xinghe-image而非Pollinations.ai（中文渲染强、免费、不翻墙）
- Updated: index.md（新增4条目，Total pages: 11）

## [2026-04-25] ingest | 每日知识整理（2026-04-24对话回收）
- 来源：2026-04-24 的 5 个对话（飞书×1、微信×1、CLI×1、Cron×2）
- 新建页面：
  - entities/open-webui.md（开源LLM前端，Docker部署+超时配置经验）
  - entities/xianyu-monitor.md（闲鱼监控工具，AI筛选二手好物）
  - concepts/wechat-ilink-token.md（微信iLink Token过期机制）
- 更新页面：
  - concepts/wechat-publishing-toolchain.md（新增实战经验：bm.md API踩坑、发布流程验证）
- 更新：index.md（新增3条目，Total pages: 14）

## [2026-04-25] create | wechat-cli 安装与配置
- 新增页面：
  - entities/wechat-cli.md（开源微信本地数据库解密CLI工具，安装/重签/踩坑全记录）
- 背景：安装 wechat-cli 让 Hermes 能直接读取微信聊天数据
- 安装微信 4.1.8（brew cask 缓存）+ 重签 get-task-allow + wechat-cli init
- 踩坑：SIP阻止codesign需/tmp中转、sudo管道密码、macOS权限弹窗

## [2026-04-26] ingest | 每日知识整理（2026-04-25对话回收）
- 来源：2026-04-25 的 5 个对话（飞书×1、微信×1、CLI×2、Cron×1）
- 主要话题：
  1. wechat-cli 安装微信4.1.8 + 重签 + key提取成功（飞书）
  2. GenericAgent 框架调研 + DeepSeek V4定价 + GLM CodingPlan兼容性（微信）
  3. GenericAgent教程文章评价 + 公众号发布尝试（CLI×2，未完成）
  4. GLM-5.1 vs DeepSeek-V4-Pro 详细基准对比（飞书）
- 新建页面：
  - entities/generic-agent.md（自主进化AI Agent框架，9个原子工具，MixinSession容错）
  - comparisons/llm-model-comparison.md（GLM-5.1 vs DS-V4-Pro：规格/基准/定价/场景推荐）
- 更新：index.md（新增2条目，Total pages: 16）

## [2026-04-26] update | 公众号写作工具链实战经验补充
- 更新页面：
  - concepts/wechat-publishing-toolchain.md（新增：长文章拆分策略、文章写作要求、deepseek fallback问题、生图模式建议）
- 背景：GenericAgent教程文章发布失败的复盘经验 + 用户反馈文章写作改进方向
- 来源：2026-04-26 的 3 个对话（微信×1、飞书×1、Cron×1）

## [2026-04-27] create | 每日知识整理（2026-04-26对话回收）
- 来源：2026-04-26 的多个对话（B站字幕提取、Remotion动画、VPS代理选型、Playwright skill）
- 新建页面：
  - entities/bilibili-subtitle-extraction.md（B站字幕提取工具调研：bilibili-api SDK踩坑、SESSDATA方案、工具推荐Top4）
  - entities/remotion.md（Remotion视频动画框架：LoserCard卡片翻转动画V1/V2、安装踩坑、渲染配置）
  - comparisons/vps-proxy-comparison.md（VPS代理选购对比：VMISS/DMIT/搬瓦工/raksmart，结论VMISS性价比最高）
- 更新页面：
  - entities/hermes-agent.md（新增 Playwright-CLI Skill 章节：浏览器自动化、持久化Chrome Profile、4x Token节省）
- 更新：index.md（新增3条目，Total pages: 19）

## [2026-04-27] update | 补充4/26遗漏对话（微信+CLI）
- 背景：早6点cron只回收了飞书对话，遗漏微信和CLI的内容，手动补充
- 来源：2026-04-26 的 7 个对话（飞书×3、微信×1、CLI×1、Cron×2）
- 新建页面：
  - entities/hackingtool.md（GitHub 64.8k⭐安全测试工具合集，185+工具，20分类）
- 更新页面：
  - entities/generic-agent.md（新增：公众号分篇发布实战经验、浏览器控制调研、hackingtool关联）
- 更新：index.md（新增1条目，Total pages: 20）

## [2026-04-28] ingest | 每日知识整理（2026-04-27对话回收）
- 来源：2026-04-27 的 6 个对话（飞书×3、CLI×1、Cron×2、微信×0）
- 主要话题：
  1. TMWebDriver浏览器控制方案部署与集成（CLI，延续自4/26）
  2. VPS新加坡节点调研 — VMISS无新加坡节点，LightNode/Vultr/ExtraVM替代（飞书）
  3. 每日知识Cron平台覆盖缺陷发现与修复（飞书）
  4. 网络故障排查 — ping 8.8.8.8 超时（飞书，deepseek-v4-pro模型）
  5. 闲鱼Mac Studio监控播报（Cron 9PM）
  6. 每日知识整理处理4/26数据（Cron 6AM）
- 新建页面：
  - entities/tmwebdriver.md（Chrome扩展+WebSocket浏览器控制方案，三层架构详解）
- 更新页面：
  - comparisons/vps-proxy-comparison.md（新增新加坡节点补充调研：LightNode/Vultr/ExtraVM）
  - entities/generic-agent.md（新增TMWebDriver详解与部署信息）
- 更新：index.md（新增1条目，Total pages: 21）

## [2026-04-29] ingest | 每日知识回收（回收 2026-04-28 对话）
- 回收 9 个会话（CLI 4个、Feishu 3个、Cron 2个）
- 新建页面：
  - entities/opencli.md — 通用CLI Hub，90+网站适配器，零LLM消耗
  - entities/follow-builders.md — AI Builder追踪工具，25个X账号+6播客聚合
  - concepts/deepseek-protocol-compatibility.md — DeepSeek Anthropic/OpenAI双协议兼容性
- 更新页面：
  - entities/tmwebdriver.md — 新增HTTP API调用模式、踩坑经验、Bilibili使用案例
  - index.md — 更新总页数 21→24
- 关键知识点：OpenCLI安装配置、DeepSeek回退模型协议修复、TMWebDriver实战踩坑、Follow-Builders feed数据利用

## [2026-04-30] ingest | 每日知识回收（回收 2026-04-29 对话）
- 回收 7 个会话的知识点
- 新建页面：
  - entities/ai-world-digest.md — AI世界日报自动聚合管线，collect.py + 4源 + Cron 9am
  - concepts/feishu-bot-configuration.md — 飞书Bot白名单配置陷阱（空白名单=静默丢弃）
- 更新页面：
  - concepts/deepseek-protocol-compatibility.md — 新增完整三重根因分析（base_url + api_mode + adapter源码patch）、HTTP 400 "thinking must be passed back" 详细修复
  - entities/opencli.md — 新增B站评论API章节（Shadow DOM绕过、bili_jct CSRF提取、api.bilibili.com POST）
  - entities/hermes-agent.md — 新增Cron环境调试技巧（环境变量不可见、python3 -c绕过、DeepSeek超时、调试检查清单）
  - index.md — 新增2条目，Total pages: 24→26
- 关键知识点：DeepSeek fallback HTTP 400三重根因修复、B站Shadow DOM评论API、飞书白名单静默丢弃、AI世界日报管线

## [2026-05-01] ingest | 每日知识回收（回收 2026-04-30 对话）
- 回收 4 个会话（Cron×1、Feishu×2、CLI×1）
- 主要话题：
  1. 每日知识整理处理4/29数据（Cron 6AM）
  2. 公众号文章自评分88/100，差2分未达A级（Feishu 8:17AM + 10:05AM）
  3. Hermes Agent v0.10.0 → v0.11.0 升级，5个合并冲突解决（CLI 10:33PM）
- 新建页面：
  - concepts/wechat-article-scoring.md — 公众号文章八维度质量评分体系（选题20%/标题10%/结构15%/信息20%/语言10%/视觉10%/互动5%/合规10%），≥90分A级方可发布
- 更新页面：
  - entities/hermes-agent.md — 新增v0.11.0升级记录（上游吸收DeepSeek检测/自定义补丁重应用/升级经验教训）
  - concepts/wechat-publishing-toolchain.md — 新增文章质量评分章节、bm.md流程图上传经验
  - index.md — 新增1条目，Total pages: 26→27
- 关键知识点：Hermes v0.11.0升级与合并冲突解决策略、公众号文章评分门禁、delegate_task中断风险

## [2026-05-02] ingest | 每日知识回收（回收 2026-05-01 对话）
- 回收 5 个会话（Cron×3、WeChat×2）
- 主要话题：
  1. 6AM知识库Cron任务因`cfg_get` ImportError失败，手动重触发执行（Cron 10:45AM）
  2. 检查定时任务状态，发现两个Cron同时失败，排查agent.log定位根因（WeChat 10:03AM）
  3. 对AI世界日报文章进行八维度评分（88.5分B+级），用户修正发布流程（WeChat 10:33AM）
  4. 每日知识整理处理4/30数据，Wiki 26→27页（Cron 10:45AM）
- 更新页面：
  - entities/hermes-agent.md — 新增Cron `cfg_get` ImportError事件记录（根因分析、解决方案、经验教训）
  - concepts/wechat-article-scoring.md — 新增用户修正版评分流程（用户审核不可跳过）、实战评分案例
  - entities/ai-world-digest.md — 新增质量评估记录（88.5分B+级）
- 更新：index.md（更新日期），log.md（本条记录）
- 关键知识点：Gateway重启后cfg_get函数丢失导致Cron全面瘫痪、公众号文章发布流程必须有用户审核环节

## [2026-05-03] ingest | 每日知识回收（回收 2026-05-02 对话）
- 回收 2 个 Cron 会话（6AM知识库 + 9AM AI世界日报）
- 主要话题：
  1. 6AM知识库Cron成功回收5/1对话，更新Wiki 27页→30页，GitHub同步，公众号草稿上传（Cron 6:00AM）
  2. AI世界日报5/2刊采集：Codex升级、Claude Security公测、Open Design开源、Karpathy三大范式（Cron 9:00AM）
- 新建页面：
  - entities/claude-security.md — Anthropic AI代码安全审计工具，基于Opus 4.7，无需API
  - entities/open-design.md — 开源AI设计工具（nexu-io），11.8k⭐，71种品牌级设计系统
  - concepts/karpathy-llm-paradigms.md — Karpathy在红杉Ascent大会分享LLM三大新范式
- 更新页面：
  - entities/ai-world-digest.md — 新增5/2采集记录
  - index.md — 新增3条目，Total pages: 27→30
- 关键知识点：Claude Security发布、Open Design开源设计工具、Karpathy LLM三大范式（.md替代.sh/非结构化计算/菜单应用吞噬）、Codex非编码能力扩展

## [2026-05-03] ingest | 逛逛GitHub「快瞧瞧 4 月 GitHub 上哪些开源项目最火火火火？」
- Raw source: raw/articles/guangguang-github-april-hot-2026.md
- 来源：微信公众号「逛逛GitHub」4月热门开源项目汇总（8个详细介绍 + 8个简短提及）
- 新建页面：
  - entities/rtk.md — Rust写的CLI代理，为AI Coding压缩命令输出省80-90% token
  - entities/archon.md — AI编码工作流引擎，YAML定义确定性流程
  - entities/ai-edge-gallery.md — Google端侧AI展示应用，手机离线跑大模型
  - entities/ppt-master.md — AI生成可编辑PPTX，22个示例309页
  - entities/litert-lm.md — Google端侧大模型推理框架，全平台GPU/NPU加速
  - entities/matt-pocock-skills.md — Claude Code Skills合集，针对AI编程4个失败模式
- 更新页面：
  - entities/generic-agent.md — Stars更新（6.9k→8.4k），新增来源引用
  - index.md — 新增6条目，Total pages: 30→36
- 关键知识点：RTK省token方案（压缩命令输出）、Archon确定性AI编码流程、Google端侧AI双产品（Gallery+LiteRT-LM）、PPT Master原生PPTX生成、Matt Pocock Skills的4个失败模式框架

## [2026-05-04] ingest | 每日知识回收（回收 2026-05-03 对话）
- 回收 3 个会话的知识点（Feishu PPT Master + ACP Open Design SafeTech + AI世界日报 5/3刊）
- 主要话题：
  1. PPT Master 环境搭建：pycairo 构建修复（pkgconf）、UV venv Python 3.13、Hermes skill 创建
  2. Open Design SafeTech 暗色主题落地页：CSS 变量暗色方案、accent budget 规则、honest omission 原则
  3. AI世界日报 5/3 热门项目：VS Code Copilot Co-Author 争议、mike 法律 AI、whatcable USB-C、软著生成器等
- 新建页面：
  - entities/dictionary-of-ai-coding.md — mattpocock AI编程术语词典，677⭐
  - entities/software-copyright-skill.md — 软著申请生成器，636⭐
  - entities/whatcable.md — macOS USB-C线缆测试工具，1258⭐
  - entities/mike-legal-ai.md — 开源AI法律平台，1413⭐
  - concepts/vscode-copilot-coauthor.md — VS Code Copilot 自动 Co-Authored-by 争议，682pts HN
  - concepts/llm-refusal-direction.md — LLM拒绝行为单一方向控制研究，88pts HN
- 更新页面：
  - entities/ppt-master.md — 新增环境搭建记录（pycairo/pkgconf修复、UV venv路径、核心依赖表、生成管线、v2.5.0特性）
  - entities/open-design.md — 新增暗色主题技术方案（CSS变量映射、accent budget、honest omission、P0 checklist、5-dim critique）
  - index.md — 新增6条目，Total pages: 36→43
- 关键知识点：pycairo构建需pkgconf、PPT Master八项确认BLOCKING管线、Open Design暗色6变量方案、accent每屏≤2次、LLM拒绝行为单一方向控制、Copilot虚假归因争议

## [2026-05-05] ingest | 每日知识回收（回收 2026-05-04 对话）
- 回收 2026-05-04 的多个对话知识点
- 主要话题：
  1. MemPalace 开源 AI 记忆系统调研（宫殿式结构、ChromaDB 向量存储、MCP 支持）
  2. DeepSeek Fallback 教程文章撰写（GLM→DeepSeek 自动切换，三个必踩的坑）
  3. B站字幕工具全面深度调研（30+项目梳理，五大类分类，AI Agent 集成推荐）
  4. ABC安全文件爬虫脚本开发（hseffyun_spider.py，Playwright-CLI 采集）
  5. AI世界日报 5/4 采集（MemPalace 5万⭐等热点）
- 新建页面：
  - entities/mempalace.md — 本地优先的开源AI记忆系统，5万⭐，宫殿式语义搜索
  - entities/hseffyun-spider.md — ABC安全文件爬虫，基于Playwright-CLI批量采集
  - concepts/deepseek-fallback-best-practice.md — DeepSeek Fallback 配置最佳实践（3步10分钟）
- 更新页面：
  - entities/bilibili-subtitle-extraction.md — 新增深度调研（30+项目梳理、五大类分类、AI Agent集成推荐Top3）
  - concepts/wechat-publishing-toolchain.md — 新增DeepSeek Fallback教程文章写作记录
  - entities/hermes-agent.md — 新增记忆方案调研（MemPalace vs Hindsight）和安全生产工具链章节
  - concepts/deepseek-protocol-compatibility.md — 新增fallback最佳实践页面互链
  - entities/ai-world-digest.md — 新增5/4采集记录
- 清理：移除 wiki 根目录 MemPalace.md（已迁移至 entities/）
- 更新：index.md（新增3条目，Total pages: 43→46）
- 关键知识点：MemPalace宫殿式记忆架构、DeepSeek fallback三个必踩坑（base_url/api_mode/重启）、B站CC字幕API完整文档、hseffyun安全文档批量采集方案


## [2026-05-05] ingest | 每日知识回收（回收 2026-05-04 对话）
- 回收 3 个会话的知识点（Feishu 涨粉方案 + AI世界日报 5/4刊 + 知识库Cron 5/4执行）
- 主要话题：
  1. AI智管局一周涨粉100人方案：品牌定位「AI工具质检局」，全平台矩阵（公众号+抖音+小红书+知乎+B站+快手），Remotion生成竖版短视频
  2. AI世界日报5/4刊：Sam Altman称GPT-5.5 xhigh真香、OpenAI o1急诊诊断67%超越医生、DeepClaude项目降低17倍成本、Ollama v0.23.0支持Claude Desktop
  3. 知识库Cron 5/4成功回收5/3对话
- 新建页面：
  - entities/deepclaude.md — DeepSeek V4 Pro + Claude Code Agent组合，成本降低17倍
  - entities/ollama.md — 本地LLM运行工具，v0.23.0新增Claude Desktop集成
  - concepts/multi-platform-content-strategy.md — 全平台内容运营策略（一条内容→六种形态）
  - entities/mempalace.md — 本地优先AI记忆系统（子agent创建）
  - entities/hseffyun-spider.md — ABC安全文件爬虫（子agent创建）
  - concepts/deepseek-fallback-best-practice.md — DeepSeek Fallback配置最佳实践（子agent创建）
- 更新页面：
  - entities/ai-zhiguanju.md — 新增品牌定位升级、全平台矩阵、视频制作方案、涨粉计划
  - entities/ai-world-digest.md — 新增5/4采集记录
  - entities/remotion.md — 子agent新增深度调研内容
  - index.md — 新增条目，Total pages: 43→48
- 关键知识点：AI工具质检局定位、OpenCLI支持抖音/小红书/知乎、Remotion视频模板化、DeepClaude低成本Agent方案、Ollama+Claude Desktop集成

## [2026-05-06] ingest | 每日知识回收（回收 2026-05-05 对话）
- 回收 4 个会话的知识点（每日知识Cron 5/5 + AI世界日报 5/5 + 股市研究 + OpenWebUI/gpt2api部署）
- 主要话题：
  1. gpt2api (KleinAI) 部署：将ChatGPT/Grok封装为OpenAI兼容API，Docker Compose部署
  2. Docker Hub 中国镜像源配置经验（OrbStack代理陷阱）
  3. OpenWebUI 账户创建踩坑（auth+user双表插入）
  4. AI世界日报5/5刊：Agent生态成熟、AI安全关注、开源持续发力
  5. 股市研究：A股4/30收盘、美股5/4 Meta盘后跌7%、港股5/5数据
- 新建页面：
  - entities/gpt2api.md — ChatGPT/Grok封装为OpenAI兼容API网关
  - concepts/docker-china-mirrors.md — Docker Hub中国镜像源配置经验
- 更新页面：
  - entities/open-webui.md — 新增账户创建踩坑、WebSocket配置、gpt2api集成
  - entities/ai-world-digest.md — 新增5/5采集记录（74条数据）
  - index.md — 新增2条目，Total pages: 48→50
- 关键知识点：gpt2api私建API网关、OrbStack daemon不走系统VPN、OpenWebUI auth+user双表要求

## [2026-05-07] ingest | 每日知识回收（回收 2026-05-06 对话）
- 回收 3 个会话的知识点（DeepClaude部署 + AI智管局冷启动 + 每日知识Cron）
- 主要话题：
  1. DeepClaude 本地安装部署：aattaran/deepclaude 1329⭐，MIT，安装到 /Volumes/DevSSD/Applications/deepclaude/，配置到 /usr/local/bin/deepclaude
  2. AI智管局公众号冷启动诊断：定位跑偏/无传播点/单渠道零矩阵三大问题，逛逛GitHub爆款拆解，新方向「普通人能用AI干什么」
  3. 每日知识Cron前一天执行：Wiki 48→50页
- 新建页面：
  - concepts/wechat-content-strategy.md — 公众号冷启动策略与内容运营方法论（对标分析、标题公式7种、逛逛GitHub爆款拆解、排版极简主义）
- 更新页面：
  - entities/deepclaude.md — 新增本地部署记录（安装路径、CLI配置、已知bug：Issue#3/不支持图片/MCP不兼容/macOS benchmark兼容性）
  - entities/ai-zhiguanju.md — 新增冷启动诊断（三大核心问题、逛逛GitHub对标分析、内容方向调整）
  - index.md — 新增1条目，Total pages: 50→51
- 关键知识点：DeepClaude环境变量重定向API原理、公众号标题7种公式、逛逛GitHub爆款五步结构、证据型截图vs装饰型截图

## [2026-05-08] ingest | 每日知识回收（回收 2026-05-07 对话）
- 回收知识点：SOUL.md Agent人格定义、Mercury Agent调研、Agent SOUL架构概念
- 新建页面：
  - entities/soul-md.md — SOUL.md AI Agent人格定义方法论（Tony Simons 170行框架）
  - entities/mercury-agent.md — Soul-driven轻量AI Agent，多文件人格定义+结构化记忆
  - concepts/agent-soul-architecture.md — Agent SOUL架构概念（单文件vs多文件两种路径）
- 更新页面：
  - entities/hermes-agent.md — 新增SOUL.md配置记录、Mercury Agent对比、记忆系统局限分析、飞书配对命令
  - index.md — 新增3条目，Total pages: 51→54
- 关键知识点：SOUL.md反对义务和双向问责设计、Mercury多文件人格分离vs Hermes单文件大而全、Hermes记忆系统98%使用率逼近上限

## [2026-05-09] ingest | 每日知识回收 (2026-05-08)
- 回收 3 个对话会话（飞书公众号写作风格调整×1、AI世界日报5/8×1、每日知识cron×1）
- 新建页面：
  - entities/ds4.md — antirez的Mac本地DeepSeek 4 Flash Metal推理引擎
  - entities/alphaevolve.md — DeepMind的Gemini驱动编码Agent
  - concepts/wechat-writing-style.md — 公众号写作风格方法论（真人口吻、一句一段、证据型截图、冲突标题）
- 更新页面：
  - entities/hermes-agent.md — 新增Claude竞品动态（Dreaming/Outcomes功能、Anthropic 80x增长、HuggingFace恶意软件警告、Chrome隐私声明变更）
  - entities/ai-zhiguanju.md — 新增写作风格调整进展（第二轮深度分析、文章版本迭代V1→V3、对标差距总结）
  - concepts/wechat-content-strategy.md — 新增第二轮深度分析（逛逛GitHub本质揭秘、AI智管局vs逛逛GitHub差距对比表、写作风格要点提炼）
- 更新：index.md（新增3条目，Total pages: 54→57），log.md（本条记录）
- 关键知识点：逛逛GitHub本质是推荐开源项目+贴截图无实测、Claude Dreaming Agent自学习、Anthropic 80x增长与SpaceX合作、ds4 Metal本地推理、AlphaEvolve Gemini编码Agent

## [2026-05-10] ingest | 每日知识回收（回收 2026-05-09 对话）
- 回收 3 个会话的知识点（AI世界日报5/9 + 飞书yao-open-prompts调研/公众号文章/自动回复 + 每日知识cron）
- 主要话题：
  1. yao-open-prompts 项目调研：中文AI提示词库，1392⭐，116个提示词，9大分类，元提示词系统
  2. 公众号文章生成：基于yao-open-prompts撰写文章上传草稿箱
  3. 公众号自动回复配置：关键词「AI工具」→ GitHub仓库链接引流
  4. ai-toolkit仓库确认：已创建（5月6日），4个文件
- 新建页面：
  - entities/yao-open-prompts.md — 中文AI提示词库，1392⭐，116个提示词，元提示词系统
  - concepts/wechat-auto-reply.md — 公众号关键词自动回复配置经验
- 更新页面：
  - entities/ai-zhiguanju.md — 新增yao-open-prompts文章与自动回复配置（2026-05-09）
  - index.md — 新增2条目，Total pages: 57→59
- 关键知识点：yao-open-prompts三天爆火说明中文AI提示词需求旺盛、公众号自动回复配合GitHub仓库做资料引流、ai-toolkit仓库作为公众号回复下载站

## [2026-05-11] ingest | 每日知识回收（回收 2026-05-10 对话）
- 回收 5 个会话的知识点（AIHOT信源工具、Mirage项目调研、Cron文章质量修复、公众号写作硬性检查、每日知识cron）
- 新建页面：
  - entities/aihot.md — AI信源聚合工具，160+信源，数字生命卡兹克开源，API免费
  - entities/mirage.md — 统一虚拟文件系统（strukto-ai），1701⭐，TypeScript，Apache 2.0
- 更新页面：
  - concepts/wechat-writing-style.md — 新增5项硬性检查清单（2026-05-10总结），扩展为强制门禁
  - entities/ai-zhiguanju.md — 新增AIHOT信源集成记录、Mirage文章尝试、Cron质量修复记录
  - index.md — 新增2条目，Total pages: 59→61
- 关键知识点：
  1. AIHOT信源工具：160+信源抓取AI动态，API需浏览器UA，Cron 8:30推飞书
  2. Mirage项目：4天1701⭐，Issues #16并发隔离 #15 Snapshot限制，核心贡献者zechengz
  3. Cron质量修复根因：skills列表缺少ai-zhiguanju，导致生成内容缺领域知识
  4. 写作5项硬性检查：标题冲突/一段两句/证据截图/不像AI/有争议点

## [2026-05-12] update | 每日知识回收（回收 2026-05-11 对话）
- 回收 gpt2api (KleinAI) 部署调试深度知识
- 更新页面：
  - entities/gpt2api.md — 新增 Mock Mode Bug、Docker容器代理配置、端口表、Provider Factory代码位置、未解决问题
- 新建页面：
  - entities/proxytunnel.md — Nextin Chrome代理扩展，utun4 VPN隧道，7890端口
- 更新：index.md（新增1条目，Total pages: 61→62），log.md（本条记录）
- 关键知识点：
  1. Mock Mode Bug：dev-full 的 YAML anchor 优先级高于 server，导致 provider 全为 mock
  2. Docker 容器代理：daemon 代理只影响 pull，容器运行时需手动配置 HTTP_PROXY/HTTPS_PROXY
  3. ProxyTunnel：Chrome 扩展创建 utun4 隧道，7890 端口，容器通过 host IP 访问
  4. FlareSolverr 502、ChatGPT token 过期等未解决问题

## [2026-05-13] ingest | 每日知识回收（回收 2026-05-12 对话）
- 回收 3 个会话的知识点（CLI爆款复盘 + 飞书gpt2api调试 + AIHOT速报）
- 新建页面：
  - entities/chatgpt-5-5-pro.md — OpenAI 高端模型，解决菲尔兹奖级别数学题
  - entities/deepseek-v4-pro.md — DeepSeek V4 Pro 推理模型排行榜第一
  - entities/anthropic-valuation.md — Anthropic 估值动态，2026-05-12 达1.4万亿
  - concepts/small-model-orchestration.md — 小模型指挥大模型（AI权力倒挂）范式
- 更新页面：
  - entities/gpt2api.md — 新增 2026-05-12 飞书会话记录（mock mode/proxy 继续调试）
  - entities/yao-open-prompts.md — 新增爆款文章写作经验回顾、cron 质量下降根因分析
  - entities/aihot.md — 新增 2026-05-12 AIHOT 速报精选4条动态
  - concepts/wechat-content-strategy.md — 新增「116个免费中文AI提示词」爆款复盘、cron 质量问题根因
- 更新：index.md（新增4条目，Total pages: 62→66），log.md（本条记录）
- 关键知识点：
  1. ChatGPT 5.5 Pro 解菲尔兹奖级别数学题，AI 数学推理重大突破
  2. Anthropic 估值达1.4万亿，AI安全导向公司获资本市场高度认可
  3. 7B模型指挥大模型成为新范式，成本/延迟/隐私全面优于传统架构
  4. DeepSeek V4 Pro 推理排行榜第一，中国 AI 模型竞争力领先
  5. 「116个免费中文AI提示词」爆款复盘：标题公式+热点同步+流量窗口
  6. Cron 文章质量下降根因：缺少 ai-zhiguanju skill 导致无领域知识约束

## [2026-05-14] ingest | 每日知识回收（回收 2026-05-13 对话）
- 回收 AIHOT 速报 5/13 及用户对话知识点
- 新建页面：
  - entities/claude-opus-4-7.md — Anthropic 最新模型，Fast Mode 研究预览，API + Claude Code 双渠道
  - entities/step-image-edit-2.md — 3.5B 参数图像编辑模型，KRIS-Bench 基准测试第一
  - entities/google-android-intelligence.md — Google Android AI 智能功能，跨应用多步自动化 + AI 增强鼠标指针
  - concepts/ai-seeding-note-lawsuit.md — 首例 AI 生成种草笔记诉讼案，工具提供方被判赔 10 万 RMB
  - concepts/statewright-ai-constraint.md — Statewright 方法论，状态机约束 AI Agent 准确率从 2/10 到 10/10
- 更新页面：
  - entities/aihot.md — 新增 2026-05-13 AIHOT 速报精选 5 条动态
- 更新：index.md（新增5条目，Total pages: 66→71），log.md（本条记录）
- 关键知识点：
  1. Claude Opus 4.7 Fast Mode 研究预览发布，Anthropic 持续迭代高端模型矩阵
  2. Step Image Edit 2 以 3.5B 参数登顶 KRIS-Bench，中等模型专项任务优势
  3. Google Android Intelligence 将 AI Agent 范式带入移动系统层，跨应用自动化里程碑
  4. 中国首例 AI 种草笔记诉讼案判决，工具提供方承担法律责任，划清 AI 生成内容法律边界
  5. Statewright 方法论证明结构化约束（状态机）可将 AI Agent 准确率从 20% 提升到 100%

## [2026-05-16] ingest | 每日知识回收（回收 2026-05-15 对话）
- 回收 2026-05-15 对话的知识点
- 主要话题：
  1. ima2-gen 项目调研：ChatGPT 网页生图 API 封装工具（lidge-jun/ima2-gen, ⭐213）
  2. 3DCellForge 项目调研：AI 3D 模型生成工具（huangserva/3DCellForge, ⭐2058）
  3. Hermes 模型切换修复：/model 命令只改 model.default 不改 base_url/api_key/context_length，创建 switch_model.py 脚本解决
  4. 飞书全员共享：FEISHU_ALLOW_ALL_USERS=true，应用发布到企业工作台（cli_a96e813225785cdd），配对机制保留
- 新建页面：
  - entities/ima2-gen.md — ChatGPT 网页生图 API 封装工具，gpt-image-2 本地 API
  - entities/3dcellforge.md — AI 3D 模型生成工具，React+Three.js，多 provider 支持
  - concepts/model-switching-workflow.md — Hermes 模型切换工作流（/model 缺陷与 switch_model.py 方案）
- 更新页面：
  - entities/hermes-agent.md — 新增模型切换修复（2026-05-15）、飞书全员共享配置
  - concepts/feishu-bot-configuration.md — 新增 FEISHU_ALLOW_ALL_USERS=true 配置、飞书应用发布流程、配对码批准命令
- 更新：index.md（新增3条目，Total pages: 71→75），log.md（本条记录）
- 关键知识点：
  1. ima2-gen 将 ChatGPT gpt-image-2 封装为本地 API，常见失败：OAuth 过期/额度限流/Cloudflare 403/SSE 解析失败
  2. 3DCellForge 支持 Hyper3D/Tripo/Fal.ai/Hunyuan3D 四个 provider，上传图片生成 3D 模型
  3. /model 命令只更新 model.default，switch_model.py 从 custom_providers 复制完整元数据，需重启 session 生效
  4. FEISHU_ALLOW_ALL_USERS=true 开放全员使用，配对码机制仍保留控制

## [2026-05-17] ingest | 每日知识回收（回收 2026-05-16 AIHOT 速报）
- 回收 AIHOT 2026-05-16 速报精选内容
- 新建页面：
  - entities/lark-cli.md — 飞书开源命令行工具，45天GitHub破万星，AI可通过CLI操作飞书
  - entities/anthropic-valuation-2026.md — Anthropic估值3个月飙升至$900B，ARR达$45B
- 更新页面：
  - entities/aihot.md — 新增 2026-05-16 速报精选内容，补充 API 字段说明（无 score 字段，mode=selected 即精选）
- 更新：index.md（新增2条目，Total pages: 75→77），log.md（本条记录）
- 关键知识点：
  1. 飞书 Lark CLI 开源45天破万星，国内首个破万星办公套件开源项目，允许AI命令行操作飞书
  2. Lark CLI 与 MCP 模式形成对比：可见可控 vs 云端黑盒
  3. Anthropic 估值3个月飙升至 $900B，ARR $45B，企业级AI商业化能力极强
  4. AIHOT API 确认无 score 字段，mode=selected 即精选内容
