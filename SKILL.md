---
name: one-mail
description: 统一邮箱管理工具，支持 Gmail、Outlook 和网易邮箱。从单一 CLI 界面管理多个邮箱账户。适用于：管理多个邮箱账户、跨账户搜索、自动化邮件处理、脚本集成邮件功能。
---

# one-mail | 统一邮箱管理工具

统一管理 Gmail、Outlook 和网易邮箱的命令行工具。

## 快速开始

```bash
# 初始化配置
bash scripts/setup.sh

# 收取所有账户的邮件
bash scripts/fetch.sh

# 发送邮件
bash scripts/send.sh \
  --to "recipient@example.com" \
  --subject "Hello" \
  --body "Email content"
```

## 功能特性

- **多账户管理** - Gmail、Outlook、网易邮箱（163.com）
- **统一界面** - 单一 CLI 管理所有账户
- **跨账户搜索** - 在所有账户中搜索邮件
- **附件支持** - 发送和接收附件
- **JSON 输出** - 易于脚本集成
- **安全存储** - OAuth 2.0 和加密凭证

## 支持的邮箱提供商

### Gmail
- OAuth 2.0 认证
- 需要：`gog` CLI（可选）
- 功能：收取、发送、搜索、附件

### Outlook
- OAuth 2.0 认证
- Microsoft Graph API
- 功能：收取、发送、搜索、附件（< 3MB）

### 网易邮箱（163.com）
- IMAP/SMTP + 应用密码
- 自动 IMAP ID 支持
- 功能：收取、发送、搜索、附件

## 配置

配置文件存储在 `~/.onemail/`：

- `config.json` - 账户设置
- `credentials.json` - 加密凭证（600 权限）

## 使用方法

### 收取邮件

```bash
# 收取所有账户的邮件
bash scripts/fetch.sh

# 只看未读邮件
bash scripts/fetch.sh --unread

# 搜索邮件
bash scripts/fetch.sh --query "AI agent"

# 指定账户
bash scripts/fetch.sh --account gmail

# 限制数量
bash scripts/fetch.sh --limit 10
```

### 发送邮件

```bash
# 使用默认账户发送
bash scripts/send.sh \
  --to "recipient@example.com" \
  --subject "Hello" \
  --body "Email content"

# 指定账户
bash scripts/send.sh \
  --account outlook \
  --to "recipient@example.com" \
  --subject "Report" \
  --body "See attachment"

# 带附件
bash scripts/send.sh \
  --to "recipient@example.com" \
  --subject "Report" \
  --body "See attachment" \
  --attach "/path/to/file.pdf"
```

### 账户管理

```bash
# 列出所有账户
bash scripts/accounts.sh list

# 添加账户
bash scripts/accounts.sh add

# 删除账户
bash scripts/accounts.sh remove <account_id>

# 设置默认账户
bash scripts/accounts.sh set-default <account_id>
```

## 脚本

所有脚本位于 `scripts/` 目录：

- `setup.sh` - 初始化配置
- `fetch.sh` - 收取邮件
- `send.sh` - 发送邮件
- `accounts.sh` - 账户管理
- `stats.sh` - 统计信息
- `onemail` - 主入口（符号链接）

## 依赖

**必需：**
- `curl` - HTTP 请求
- `jq` - JSON 处理
- `python3` - IMAP/SMTP（网易邮箱）

**可选：**
- `gog` - Gmail OAuth 2.0（推荐）

## 安装

### 方式 1：通过 ClawHub 安装（推荐）

```bash
# 安装
clawhub install one-mail

# 初始化配置
bash scripts/setup.sh
```

### 方式 2：手动安装

```bash
# 克隆仓库
git clone https://github.com/huangbaixun/one-mail.git
cd one-mail

# 初始化配置
bash scripts/setup.sh
```

## 故障排除

### Gmail 认证失败
- 确保已安装 `gog` CLI
- 运行 `gog gmail auth` 重新认证
- 检查 OAuth 2.0 凭证

### Outlook 认证失败
- 检查 Microsoft Graph API 凭证
- 确认应用权限（Mail.ReadWrite, Mail.Send）
- 重新运行 `bash scripts/setup.sh`

### 网易邮箱连接失败
- 确认已启用 IMAP/SMTP 服务
- 使用应用密码（不是登录密码）
- 检查防火墙设置

### 附件发送失败
- Outlook：文件大小 < 3MB
- 检查文件路径是否正确
- 确认文件权限可读

## 注意事项

- 配置文件包含敏感信息，不要提交到 git
- 使用 OAuth 2.0 比密码更安全
- 定期更新凭证和密码
- 备份配置文件

## 许可证

MIT License

## 作者

Huang Baixun ([@huangbaixun](https://github.com/huangbaixun))

## 相关链接

- GitHub: https://github.com/huangbaixun/one-mail
- ClawHub: https://clawhub.com/skills/one-mail
- OpenClaw: https://openclaw.ai
