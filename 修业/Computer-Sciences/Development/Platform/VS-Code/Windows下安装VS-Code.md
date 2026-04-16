# Windows下安装VS Code

Visual Studio Code（简称 VS Code）是微软推出的一款轻量但功能强大的代码编辑器。它本身是编辑器，不是完整 IDE，但通过扩展可以快速补齐大多数开发需求。
## 下载VS Code
官方地址：
- https://code.visualstudio.com/
进入官网后，Windows 用户一般直接点击 **Download for Windows** 即可，默认为最新版本，也可以根据需求选择[早期版本](https://code.visualstudio.com/docs/supporting/faq#_previous-release-versions)，不推荐直接使用最新版本。
常见下载版本：
- User Installer
  - 安装到当前用户目录
  - 不需要管理员权限
  - 适合个人电脑、最常用
- System Installer
  - 安装到系统目录
  - 通常需要管理员权限
  - 适合多人共用电脑或统一管理环境
- ZIP 版本
  - 免安装
  - 适合临时使用或特殊环境
  一般建议：
- 普通个人使用：优先选择 **User Installer**
- 需要系统级统一安装：选择 **System Installer**
## 安装步骤
双击下载好的安装程序后，按向导操作即可。
### 接受协议
- 勾选同意许可协议
- 点击“下一步”
### 选择安装位置
一般保持默认即可。
常见默认路径示例：
- User Installer  
  `$C:\Users\你的用户名\AppData\Local\Programs\Microsoft VS Code$`
- System Installer  
  `$C:\Program Files\Microsoft VS Code$`
  如果没有特殊需求，不建议随意更改路径。
### 开始安装
- 点击“安装”
- 等待安装完成
- 勾选“启动 Visual Studio Code”
- 点击“完成”
## 验证是否安装成功

### 从开始菜单启动
- 按 `Win`
- 搜索 `Visual Studio Code`
- 点击打开
如果能正常启动，说明基本安装成功。
### 桌面或任务栏启动
如果安装时创建了快捷方式，也可以直接从桌面或任务栏打开。
### 终端检查 `code` 命令
打开：
- PowerShell
- Windows Terminal
- CMD
输入：
``` powershell
code --version
```
如果正常输出版本号，说明 PATH 配置成功。
## 如果code命令不能用怎么办
有时 VS Code 已安装成功，但终端中输入 `code` 无效，常见原因如下。
### 安装时没有勾选 PATH
- 重新运行安装程序并勾选“添加到 PATH”
- 或者卸载后重新安装
### 终端没有刷新环境变量
- 关闭当前终端窗口
- 重新打开终端
- 再次执行 `code --version`
### 手动添加 PATH
如果确实需要手动设置，可将 VS Code 安装目录加入系统环境变量。
常见路径：
``` powershell
C:\Users\你的用户名\AppData\Local\Programs\Microsoft VS Code\bin
```
或者：

``` powershell
C:\Program Files\Microsoft VS Code\bin
```

添加完成后重新打开终端测试：

``` powershell
code --version
```
## 首次启动后建议做的事

VS Code 安装完成后，不建议只停留在“能打开”。更好的做法是顺手完成基础配置。

### 登录设置同步（可选）
如果你有 Microsoft 或 GitHub 账号，可以启用设置同步：
- 同步扩展
- 同步主题
- 同步快捷键
- 同步设置
适合多台设备之间保持一致环境。
### 安装中文语言包（可选）
如果更习惯中文界面，可以安装：
- Chinese (Simplified) Language Pack for Visual Studio Code
安装后按提示重启 VS Code 即可。
### 安装常用扩展
常用扩展示例：
- Chinese Language Pack
- Python
- R
- Pylance
- Jupyter
- C/C++
- Live Server
- Prettier
- Markdown All in One
- GitLens

具体装哪些扩展，取决于相应开发方向。
### 打开自动保存（可选）
适合新手，避免忘记保存文件。
设置路径：
- `File > Auto Save`
也可以在设置中进一步调整自动保存策略。
## 推荐的基础设置

可以在设置界面搜索并调整以下选项：
- `Editor: Font Size`
- `Editor: Tab Size`
- `Editor: Word Wrap`
- `Files: Auto Save`
- `Editor: Format On Save`
- `Terminal Integrated Default Profile Windows`
如果你使用 Markdown 和代码较多，推荐优先关注：
- 自动保存
- 保存时自动格式化
- 自动换行
- 默认终端
## 推荐使用方式
安装完成后，更推荐按“项目”来使用 VS Code，而不是随便打开单个零散文件。
建议习惯：
- 一个项目对应一个文件夹
- 用“打开文件夹”而不是频繁单开文件
- 在项目根目录使用终端
- 配合 Git 管理代码
- 按需安装扩展，不要一次装太多
## 注意事项
不建议开启 VS Code 自动更新，主要是为了避免插件不兼容、中断工作、环境不一致等问题，尤其在生产/团队开发环境更建议关闭。
### 关闭自动更新
#### 界面设置
1. 打开设置：`Ctrl+,`（Win/Linux）/ `Cmd+,`（Mac）
2. 搜索：`update.mode`
3. 下拉选：**none**（完全关闭）或 **manual**（仅手动检查）
#### settings.json（彻底稳定）
1. `Ctrl+Shift+P` → 输入：Open Settings (JSON)
2. 添加：
```json
"update.mode": "none",
"update.enableWindowsBackgroundUpdates": false,
"extensions.autoUpdate": false
```
3. 保存重启
#### 命令行（临时禁用）
```bash
code --disable-updates
```

#VS-Code