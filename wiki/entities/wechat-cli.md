---
title: wechat-cli
created: 2026-04-25
updated: 2026-04-25
type: entity
tags: [ai-tool, automation, llm]
sources: []
---

# wechat-cli

开源命令行工具，本地解密微信 SQLCipher 数据库，让 AI 能读取微信聊天记录、联系人、收藏等数据。

## 基本信息

- GitHub: `huohuoer/wechat-cli`（432 Star, 1013 Fork）
- npm 包: `@canghe_ai/wechat-cli`（v0.2.4）
- 协议: Apache 2.0
- 官网: wesight.ai

## 安装

```bash
npm install -g @canghe_ai/wechat-cli
```

## 前置条件

1. **微信版本**: ≤ 4.1.8（我们安装的 4.1.8 build 37335，通过 Homebrew cask 缓存获取）
   - `brew info wechat` 可查看当前版本
   - Homebrew 缓存路径: `/Volumes/DevSSD/DevCache/homebrew/downloads/`
2. **重签微信**: 需要添加 `com.apple.security.get-task-allow` 权限
3. **sudo 密码**: 用户密码是 `1234`
4. **macOS 完全磁盘访问权限**: 需要给 Terminal 开启

## 重签微信流程

```bash
# 1. 杀掉微信
killall WeChat

# 2. 复制到/tmp重签（/Applications直接codesign会被SIP拒绝）
cp -R /Applications/WeChat.app /tmp/WeChat.app

# 3. 创建entitlements文件
cat > /tmp/wechat_ent.plist <<'PLIST'
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>com.apple.security.get-task-allow</key>
    <true/>
</dict>
</plist>
PLIST

# 4. 重签（在/tmp下不需要sudo）
codesign --force --sign - --entitlements /tmp/wechat_ent.plist /tmp/WeChat.app

# 5. 替换回/Applications（需要sudo）
echo '1234' | sudo -S rm -rf /Applications/WeChat.app
echo '1234' | sudo -S cp -R /tmp/WeChat.app /Applications/WeChat.app

# 6. 重启微信并登录
open /Applications/WeChat.app
```

## 初始化

```bash
echo '1234' | sudo -S wechat-cli init
```

配置文件位置: `~/.wechat-cli/`
- `config.json` — 数据目录路径
- `all_keys.json` — 解密密钥

## 常用命令

```bash
wechat-cli sessions --limit 10          # 最近会话
wechat-cli history "联系人" --limit 20  # 聊天记录
wechat-cli search "关键词"              # 搜索消息
wechat-cli contacts --query "名字"      # 搜索联系人
wechat-cli favorites                    # 收藏
wechat-cli unread                       # 未读消息
wechat-cli new-messages                 # 增量新消息
wechat-cli stats "群名"                 # 聊天统计
wechat-cli export "联系人" --format markdown  # 导出
```

## 踩坑记录

1. **微信版本必须 ≤ 4.1.8** — 最新 4.1.9 不兼容，需要从 Homebrew 缓存找旧版
2. **codesign SIP 限制** — 直接在 /Applications 下 codesign 会报 "Operation not permitted"，必须先复制到 /tmp 重签再 sudo 替换回去
3. **sudo 管道** — `echo 'pwd' | sudo -S command` 方式传密码，不能用 heredoc 同时管道 sudo
4. **macOS 弹窗** — Terminal/Node/Python3 需要手动添加"完全磁盘访问权限"：
   - 系统设置 → 隐私与安全性 → 完全磁盘访问权限 → 点 "+" 手动添加
   - Terminal: `/System/Applications/Utilities/Terminal.app`
   - Node: `/opt/homebrew/Cellar/node/25.9.0_2/bin/node`
   - Python3: `/usr/bin/python3`
   - 这些程序不在应用列表里，需要 `Cmd+Shift+G` 输入路径手动定位
5. **外置 SSD 安装** — 微信安装在 `/Applications/WeChat.app`，外置 SSD 做符号链接：`/Volumes/DevSSD/Applications/WeChat.app -> /Applications/WeChat.app`

## 与 Hermes 集成潜力

- 每日知识整理 cron 可直接读取微信聊天记录，不再仅依赖 session_search
- `new-messages` 命令可做消息监控，替代过期的 iLink Token
- 重要聊天记录可导出存入 [[Obsidian Wiki]]

## 相关

- [[wechat-publishing-toolchain]] — 公众号发布工具链
- [[wechat-ilink-token]] — 微信 iLink Token 过期机制
