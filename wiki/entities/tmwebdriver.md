---
title: TMWebDriver
created: 2026-04-28
updated: 2026-04-29
type: entity
tags: [ai-tool, agent, automation, coding]
sources: [conversation/2026-04-27]
---

# TMWebDriver

源自 [[generic-agent]] 项目的浏览器控制方案，通过 Chrome 扩展 + WebSocket/HTTP 双通道直接控制用户已打开的浏览器，无需 Playwright。

## 背景

GenericAgent 项目的核心组件之一，解决了 Playwright 无法继承用户已登录浏览器状态的问题。被集成到 [[hermes-agent]] 作为默认浏览器控制方案。

## 架构（三层）

1. **Chrome 扩展 (tmwd_cdp_bridge)** — MV3 Manifest
   - 通过 `chrome.alarms` 实现 5 秒探针 + 24 秒心跳保持 Service Worker 存活
   - 解决 MV3 中 Service Worker 自动休眠问题

2. **Python 服务器 (TMWebDriver.py)** — 本地服务
   - WebSocket 端口：`18765`
   - HTTP 端口：`18766`
   - 依赖：`simple-websocket-server`、`bottle`

3. **JS 执行双通道**
   - 主通道：`chrome.scripting.executeScript`（MAIN world）
   - 备用通道：CSP 阻挡时回退到 `chrome.debugger` + CDP `Runtime.evaluate`

## 部署路径

| 项目 | 路径 |
|------|------|
| 主目录 | `~/.hermes/tmwebdriver/` |
| 扩展资源 | `~/.hermes/tmwebdriver/assets/` |
| TMWebDriver.py | `~/.hermes/tmwebdriver/TMWebDriver.py` |
| Hermes Skill | `~/.hermes/skills/browser/tmwebdriver/SKILL.md` |

## 安装步骤

1. 安装依赖：`pip3 install simple-websocket-server bottle`
2. 部署到 `~/.hermes/tmwebdriver/`
3. Chrome 中加载扩展：`chrome://extensions/` → Load unpacked → 选择 assets 目录
4. 启动 Python 服务器
5. 验证：`ws://127.0.0.1:18765` 连接正常

## 与 Playwright 对比

| 维度 | TMWebDriver | Playwright |
|------|-------------|------------|
| 浏览器 | 用户已打开的 Chrome | 独立实例 |
| 登录状态 | ✅ 继承所有 | ❌ 需重新登录 |
| CSP 绕过 | ✅ 双通道回退 | 有限 |
| Token 消耗 | 低 | ~4x 更多 |
| 适用场景 | 日常浏览器自动化 | 测试、爬虫 |

## HTTP API 调用模式

```json
POST http://127.0.0.1:18766/link
{
  "cmd": "execute_js",
  "sessionId": "<tab_id>",
  "code": "<javascript_code>"
}
```

- 获取所有标签页：`{"cmd": "get_all_sessions"}` → `[[id, {url, title, type}], ...]`
- Session 类型：`ws`（内容脚本）、`ext_ws`（扩展后台）、`http`（长轮询）

## 踩坑经验（2026-04-28 实战补充）

1. **`jump()` 不接受 `session_id` 关键字参数** — 必须先 `driver.set_session('keyword')` 再 `jump()`
2. **内容脚本未注入**：新标签页/导航后 `execute_js` 返回 `{'data': 'remote_execute_js'}`，需刷新页面
3. **SPA 页面需等待 4-6 秒** 才能读取内容
4. **返回格式**：`execute_js()` 返回 `{'data': '...'}` 字典，非原始字符串

## Bilibili 使用案例

成功用于查看 B站消息（99+ 未读），通过 `execute_js("document.body.innerText")` 提取完整回复列表。但"收到的赞"页面因 SPA 渲染问题未成功。

- [[opencli]] 作为更优的 B站操作替代方案已部署

## 决策

2026-04-28 确定 TMWebDriver 为 [[hermes-agent]] 的**默认浏览器控制方式**，Playwright 仅在用户明确要求时使用。

## 相关

- [[generic-agent]] — TMWebDriver 的源项目
- [[hermes-agent]] — 已集成 TMWebDriver 作为浏览器控制 skill
- [[wechat-publishing-toolchain]] — 浏览器控制在公众号发布中的作用

