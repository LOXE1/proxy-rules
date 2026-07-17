# proxy-rules

个人代理分流规则仓库。仓库只保存公开的域名/IP 规则，不保存机场订阅地址、节点、密码、Token 或证书。

## Clash Verge Rev / Mihomo

首次将 `clash/clash-verge-bootstrap.txt` 的全部内容粘贴到“全局扩展脚本”，并保持“全局扩展覆写配置（Merge）”为空。

脚本会自动加载以下远程规则集，每 86400 秒检查更新：

- OpenAI
- Gemini（精确规则，不接管整个 Google/YouTube）
- Claude
- Copilot
- Discord
- Telegram
- TikTok

普通网站和 YouTube 默认继续使用订阅原始规则。`clash/rules/youtube-optional.yaml` 仅作为备用，不在默认脚本中启用。

## Quantumult X

按照 `quantumultx/bootstrap.txt` 进行一次性接入。之后 `quantumultx/managed.list` 会按 `update-interval=86400` 自动同步。

YouTube 默认不由本仓库接管；`quantumultx/youtube-optional.list` 仅作为备用。

## 修改方式

以后修改应用分流时，直接更新本仓库中的规则文件。客户端下一次同步后生效，无需重新导出、导入完整配置。
