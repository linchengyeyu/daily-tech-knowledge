# 无公网IP免费内网穿透最安全方案 Cloudflare Tunnel（含加速方案）

- 来源：微信公众号「无辣的学习笔记」（作者：无辣自由行）
- 原文链接：https://mp.weixin.qq.com/s/1BNHyFqz1lJN5pN7u6O34w
- 发布日期：2026-03-14

---

## 前言

我家里的内网穿透用的是lucky+ddns的方案，主要依赖于公网IPv6，但是公司的破网没有IPv6，Cloudflare Tunnel应该是目前零成本方案中最安全稳定的，无需公网 IP、不用端口映射、不暴露路由器，唯一的缺点是国内访问比较慢，我只使用sun panel这种页面类的服务，影响不大。但如果想穿透应用类的服务，还需要给Cloudflare Tunnel做优选ip加速，设置有点复杂，文章最后也会演示。

## Cloudflare Tunnel 配置

1. 打开 Cloudflare → Zero Trust → 网络 → 连接器 → 添加隧道
2. 创建隧道，隧道名任意
3. 选择安装方案，用docker部署在NAS上：
   - 国内用户在命令中添加 `--protocol http2` 变量，可以加快连接速度
   ```
   docker run cloudflare/cloudflared:latest tunnel --protocol http2 --no-autoupdate run --token xxx
   ```
4. 打开NAS的SSH，执行docker命令
5. 稍作等待，页面下方就会显示已连接的隧道
6. 继续设置二级域名，下方填写服务内网地址
7. 打开网址测试

## 飞牛OS设置

直接在应用商店安装 `Cloudflare Tunnel` 应用（不推荐）。

步骤：安装应用 → 创建令牌 → 填入账号ID和令牌API → 创建隧道 → 添加配置（域名+本地链接）→ 等待几分钟

> 个人建议docker安装，应用商店版本较低，且无法看到日志，操作反而更复杂。

## 加速访问

未加速前延时较高，应用类服务基本不可用。加速步骤：

1. 准备第二个域名，托管到CF上（可用免费域名）
2. 编辑已有隧道 → 添加已发布应用程序路由，域填加速域名
3. 给加速域名设置回退源，等待显示有效
4. 添加自定义主机名，主机名填主域名
5. 查看自定义主机名状态，复制验证txt名称及值
6. 在主域名中添加txt的dns解析
7. 重复操作，添加证书验证
8. 验证有效后，添加自定义主机名的DCV委派（证书自动续费）
9. 主域名新建cname解析
10. 加速域名添加加速记录（如 `www.visa.cn`，需网上自找优选IP）
11. 主域名修改解析地址为加速域名（如 `speedup.1day.us.ci`）
12. 再次测速，改善明显
