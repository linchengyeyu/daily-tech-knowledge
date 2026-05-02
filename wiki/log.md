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
