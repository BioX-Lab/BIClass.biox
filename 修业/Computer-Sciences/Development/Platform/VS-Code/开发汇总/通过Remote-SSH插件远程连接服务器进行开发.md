# 通过Remote-SSH插件远程连接服务器进行开发
##  安装VS Code
1. 打开浏览器，访问 VS Code 官方下载地址：https://code.visualstudio.com/。
2. 根据操作系统（Windows/macOS/Linux）选择对应版本下载（页面会自动匹配系统，直接点击「Download」即可）；若最新版本出现兼容性问题，可在下载页下拉选择历史版本。
## 安装Remote-SSH插件
1. 打开 VS Code，点击左侧边栏「扩展」图标（快捷键：Windows/Linux 为 `Ctrl+Shift+X`，macOS 为 `Cmd+Shift+X`）。
2. 在扩展搜索框输入 `Remote-SSH`，选择微软官方发布的插件（标注「Microsoft」，图标为 SSH 标志），点击「安装」。
3. 安装完成后，左侧边栏会自动显示「Remote Explorer」（远程资源管理器）图标（两台相连的电脑样式）。
## 直接输入SSH命令连接服务器
1. 点击左侧「Remote Explorer」图标，在面板顶部下拉菜单选择「Remotes (Tunnels/SSH)」，点击「+ Add Remote」按钮。
2. 在弹出的输入框中输入 SSH 连接命令，格式如下：
``` bash
ssh 用户名@服务器IP地址 -p 端口号
```
   - 示例（默认 22 端口）：`ssh root@192.168.1.100`（本地服务器）、`ssh ubuntu@47.98.xx.xx`（云端服务器）；
   - 示例（自定义端口）：`ssh admin@10.0.0.5 -p 2222`；
3. 按回车键后，选择 SSH 配置文件保存路径（推荐默认路径）。
4. 在 Remote Explorer 服务器列表中找到新增的服务器，右键选择「Connect to Host in New Window」。
5. 首次连接时，根据提示选择服务器系统类型（Linux/macOS/Windows），输入服务器登录密码，等待连接完成即可开始远程开发。

## 编辑SSH配置文件（推荐）
1. 按下 `F1`（或 `Cmd+Shift+P`/`Ctrl+Shift+P`）打开命令面板，输入 `Remote-SSH: Open SSH Configuration File...`，或者点击「Remote Explorer」面板中的配置图标“Open SSH Config File”，选择 `~/.ssh/config` 文件打开。
2. 在配置文件中按以下格式添加服务器信息（可自定义名称，便于区分多台服务器）：
```config
# 自定义服务器名称（如 MyCloudServer）
Host MyCloudServer
  HostName 47.98.xx.xx  # 服务器IP/域名
  User ubuntu           # 登录用户名
  Port 22               # 端口号（可选，默认22）
```
3. 保存配置文件后，Remote Explorer 列表会自动同步，后续直接点击服务器名称即可连接，无需重复输入命令。

## 配置SSH密钥对（免密登录）
### 本地生成密钥对
1. 打开本地终端（Windows 可使用 PowerShell/CMD，macOS/Linux 直接打开终端），执行命令：
``` bash
# 基础生成命令（推荐）
ssh-keygen
# 可选：添加标识（便于区分多密钥）
ssh-keygen -t rsa -C "your_email@example.com"
```
2. 按提示回车即可（无需设置密码，直接回车跳过），默认在 `~/.ssh` 目录生成：
   - `id_rsa`：私钥（切勿泄露）；
   - `id_rsa.pub`：公钥（需复制到服务器）。
###  复制公钥到远程服务器
1. 执行以下命令（替换为实际用户名和服务器IP）：
``` bash
ssh-copy-id -i ~/.ssh/id_rsa.pub 用户名@服务器IP -p 端口号
```
   - 示例：`ssh-copy-id -i ~/.ssh/id_rsa.pub ubuntu@47.98.xx.xx -p 22`；
2. 输入服务器登录密码，回车后即可完成公钥复制。
3. Windows 系统若提示 `ssh-copy-id` 命令不存在，可手动复制 `id_rsa.pub` 内容，粘贴到服务器 `~/.ssh/authorized_keys` 文件中；
### 测试免密连接
在本地终端执行 `ssh 用户名@服务器IP`，若无需输入密码即可登录，说明配置成功。
SSH密钥对配置完成后，VS Code一般可以默认免密连接到远程服务器。

## VS Code 配置免密连接（可选）
1. 确保已安装 Remote-SSH 插件，按下 `F1`（或 `Cmd+Shift+P`/`Ctrl+Shift+P`），输入 `Remote-SSH: Open SSH Configuration File...`，或者点击「Remote Explorer」面板中的配置图标“Open SSH Config File”， 并打开 `~/.ssh/config`。
2. 在配置文件中补充密钥相关配置，示例：
``` config
Host MyCloudServer
  HostName 10.211.55.4    # 服务器IP
  User bill               # 登录用户名
  Port 22                 # 端口号
  PreferredAuthentications publickey  # 优先使用公钥认证
  IdentityFile "~/.ssh/id_rsa"        # 本地私钥路径
```
3. 保存配置文件后，关闭 VS Code 重新打开，在 Remote Explorer 中点击服务器名称，即可**无需输入密码**直接连接。若存在多服务器/多密钥场景，为不同服务器配置不同的 `IdentityFile` 路径即可区分。


#VS-Code #Remote-SSH #BIClass