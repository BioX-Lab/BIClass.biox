# Windows 中安装与配置 typora-copilot

[`typora-copilot` ](https://github.com/Snowflyt/typora-copilot)是 Typora 的 AI 辅助插件，可在 Typora 中提供对话、写作辅助等能力。  

在安装 `typora-copilot` 之前，先准备以下软件：
- Typora
- Node.js
## 安装 Typora

如果尚未安装 Typora，可先前往[官网](https://typora.io/)下载并安装。安装完成后建议：
- 启动一次 Typora
- 确认 Typora 可以正常打开
- 确认本机具备正常读写用户目录的权限
## 安装 Node.js
`typora-copilot` 依赖 Node.js （版本 ≥ 20 ）运行。
### 下载 Node.js
打开[官网](https://nodejs.org/)下载安装包，通常建议选择 **LTS 版本**。
### 安装 Node.js
在 Windows 中双击安装包，按默认选项完成安装即可。  
安装过程中一般保持默认设置即可，通常会自动添加到系统 PATH。
### 验证安装
打开 PowerShell，执行：
``` powershell
node -v
npm -v
```
如果能够正常显示版本号，说明安装成功。
## 安装 typora-copilot
完成 Node.js 和 Typora 安装后，再执行插件安装。
### 执行安装命令
以管理员身份打开 PowerShell。
``` powershell
iwr -Uri "https://raw.githubusercontent.com/Snowflyt/typora-copilot/main/install.ps1" | iex
```
这条命令会：
- 从 GitHub 下载官方安装脚本
- 自动执行安装流程
### 安装完成后检查
安装完成后建议：
- 关闭 Typora
- 重新打开 Typora
- 检查插件是否已经成功加载
- 查看是否出现 typora-copilot 的入口或相关设置项
### 如果 PowerShell 提示脚本被禁止执行
有些系统会限制 PowerShell 脚本执行。如果出现类似提示，可以先执行：
``` powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```
然后重新运行安装命令。如果不希望长期修改策略，也可以先查看脚本内容，再决定是否执行。
## 安装后的配置
安装插件后，通常还需要继续配置模型服务，插件本身不直接提供大模型能力。点击Typora右下角的Copilot插件，选择”登录以认证Copilot“，根据提示进行GitHub Copilot认证。认证完成后，插件会自动连接到 Copilot 服务，之后就可以在 Typora 中使用 AI 辅助功能了。如果不喜欢自动补全，可以在插件设置选择“Disable completion”。

#Typora #typora-copilot