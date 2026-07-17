# proxy-rules

个人代理分流规则仓库。这里只保存公开的域名/IP 规则，不保存机场订阅地址、节点、密码、Token 或证书。

## 当前稳定原则

- **不拆分 Gemini、Google 和 YouTube**：全部交回订阅原始 Google/媒体规则，避免同一会话出现多出口 IP。
- **敏感应用失败即阻断**：Clash 地区组没有匹配节点时使用 `REJECT`，不回退到真实网络。
- **普通网站保持原配置**：不强制改写 TUN、DNS、GEOIP、媒体和最终分流。
- **一份规则源生成两种客户端格式**：只维护 `rules/source.json`，GitHub Actions 自动生成 Mihomo 与 Quantumult X 规则，避免两端漂移。
- **YouTube 不使用延迟自动组强制分流**：继续使用订阅原始国际媒体/国外网站策略；需要时手动选择真实带宽快的节点。

## Clash Verge Rev / Mihomo

首次或脚本结构升级时，将 `clash/clash-verge-bootstrap.txt` 的全部内容粘贴到：

`订阅 → 全局扩展脚本`

同时保持“全局扩展覆写配置（Merge）”为空。

脚本创建并管理：

- OpenAI
- Claude
- Copilot
- Discord
- Telegram
- TikTok
- 越南/泰国/美国固定端口 `10001 / 10002 / 10003`
- 香港、台湾、日本、新加坡、美国、越南、泰国、印尼、印度地区组

Gemini、Google、YouTube 不在脚本管理范围内。

建议日常使用：

- TUN：开启
- 模式：规则
- TUN Stack：mixed
- 自动路由与自动检测接口：开启
- 不额外堆叠复杂 DNS/覆写，普通网站异常时先检查连接命中规则

远程应用规则每 `86400` 秒自动检查更新。

## Quantumult X

完整配置保留在本机，节点使用 `server_remote`，应用规则使用：

`quantumultx/managed.list`

该远程规则不包含 Gemini、Google 和 YouTube。Quan X 继续让它们走原来的 Google/国际媒体/国外网站规则。

首次接入或清理旧配置请参考 `quantumultx/bootstrap.txt`。

## 单一规则源

编辑：

`rules/source.json`

随后 GitHub Actions 会运行：

`scripts/generate_rules.py`

自动生成：

- `clash/rules/*.yaml`
- `quantumultx/managed.list`

生成脚本会拒绝把 Gemini、共享 Google 服务和 YouTube 域名误加入应用分流。

## 更新与回滚

- 域名/IP 规则变化：客户端自动更新，不需要重新导入完整配置。
- 策略组、固定端口、进程规则变化：Clash 需要重新粘贴一次 bootstrap。
- Quantumult X 完整配置结构变化：重新导入一次新的完整 `.conf`。
- 出现异常时优先回滚最近一次规则提交，不继续扩大域名匹配范围。
