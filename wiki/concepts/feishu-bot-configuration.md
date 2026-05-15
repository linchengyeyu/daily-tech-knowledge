---
title: 飞书 Bot 白名单配置
created: 2026-04-30
updated: 2026-05-16
type: concept
tags: [deployment, best-practice, automation]
sources: [conversation/2026-04-29, conversation/2026-05-15]
---

# 飞书 Bot 白名单配置

飞书集成中 `FEISHU_ALLOW_ALL_USERS=false` 且 `FEISHU_ALLOWED_USERS` 为空时，所有消息会被静默丢弃，无任何报错或日志提示。

## 问题

配置飞书 Bot 应用时，消息完全无响应：
- Bot 在线状态正常
- Webhook 收到请求
- 但消息被静默丢弃，不触发 Agent 处理

## 根因

两个环境变量的组合导致静默拒绝：

```bash
FEISHU_ALLOW_ALL_USERS=false   # 不允许所有用户
FEISHU_ALLOWED_USERS=          # 白名单为空 → 无人被允许
```

逻辑是 `if not allow_all and user not in allowed_users: drop()`，白名单为空意味着所有用户都不在列表中。

## 修复

### 1. 填充白名单

```bash
# 在 .env 或部署配置中添加允许的用户 ID
FEISHU_ALLOWED_USERS=ou_xxxx,ou_yyyy,ou_zzzz
```

获取用户 ID 的方法：飞书管理后台 → 组织架构 → 点击用户 → 复制 Open ID。

### 2. 或允许所有用户（测试环境）

```bash
FEISHU_ALLOW_ALL_USERS=true
```

### 3. 发布新版本

修改环境变量后需要发布新版本的应用：

```bash
# 重新部署或重启服务
# 如果使用 Docker：docker restart <container>
# 如果使用 PM2：pm2 restart <app>
```

## 最佳实践

1. **白名单为空时应报警**：建议代码中加入检查，`ALLOW_ALL=false` 且 `ALLOWED_USERS` 为空时打印 WARNING 日志
2. **开发环境**用 `ALLOW_ALL=true`，**生产环境**用白名单
3. **静默丢弃是反模式**：至少应该在日志中记录被拒绝的消息来源

## 相关

- [[hermes-agent]] — 飞书是 Hermes 的集成渠道之一
- [[deepseek-protocol-compatibility]] — 另一个"静默失败"的配置陷阱案例

## 全员共享配置（2026-05-15）

### FEISHU_ALLOW_ALL_USERS=true

将飞书 Bot 对企业内所有用户开放：

```bash
FEISHU_ALLOW_ALL_USERS=true
```

### 飞书应用发布到企业工作台

- **应用 ID**：`cli_a96e813225785cdd`
- 发布到飞书企业工作台后，企业内所有成员均可搜索并使用 Bot
- **配对机制保留**：新用户首次使用仍需配对码，管理员通过以下命令批准：

```bash
hermes pairing approve feishu <code>
```

### 注意事项

- 全员开放适合测试和企业内部使用，不建议对公开放
- 配对码机制确保只有经过批准的用户才能实际使用 Agent
- 发布新版本需在飞书开放平台操作「创建版本」→「申请发布」
