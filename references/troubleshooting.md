# 故障排除

## Gmail

- 确保已安装 `gog` CLI
- 运行 `gog gmail auth` 重新认证
- 检查 OAuth 2.0 凭证是否过期

## Outlook

- 检查 Microsoft Graph API 凭证
- 确认应用权限包含 Mail.ReadWrite 和 Mail.Send
- 重新运行 `bash scripts/setup.sh` 刷新 token
- 附件大小限制 3MB

## 网易邮箱（163.com / 126.com）

- 确认已在邮箱设置中启用 IMAP/SMTP 服务
- 使用应用专用密码（不是登录密码）
- 检查防火墙是否放行 993(IMAP) 和 465(SMTP) 端口
- 网易要求 IMAP ID 命令，脚本已自动处理
- 163 服务器：imap.163.com / smtp.163.com
- 126 服务器：imap.126.com / smtp.126.com

## 通用问题

- 附件发送失败：检查文件路径和读取权限
- JSON 解析错误：确认 `jq` 已安装
- 配置文件位置：`~/.onemail/config.json`
- 凭证文件位置：`~/.onemail/credentials.json`（权限 600）
