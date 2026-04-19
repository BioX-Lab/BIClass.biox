# Windows下安装Node.js

Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境，广泛用于服务器端开发。这里介绍如何在 Windows 系统上安装 Node.js。

## 使用官方安装程序（推荐）
### 访问官网
前往 [Node.js 官网](https://nodejs.org/)，下载 **LTS（长期支持版）** 安装程序。
### 运行安装程序
双击下载的 `.msi` 文件，按照向导提示安装。  
建议勾选 **“Automatically install the necessary tools”** 选项，以便自动安装 npm 和配置环境变量。
### 验证安装
安装完成后，打开 **命令提示符（CMD）** 或 **PowerShell**，输入以下命令检查版本：
``` bash
node -v
npm -v
```
如果显示版本号，说明安装成功。
## 使用包管理器
如果已安装 Chocolatey 或 Scoop，可以通过一行命令安装：
- **Chocolatey**：
``` bash
choco install nodejs
```
- **Scoop**：
``` bash
scoop install nodejs
```
## 使用 nvm-windows（管理多版本）

如果需要切换不同 Node.js 版本，可以使用 [nvm-windows](https://github.com/coreybutler/nvm-windows)：
### 下载 nvm-windows
从 [发布页面](https://github.com/coreybutler/nvm-windows/releases) 下载 `nvm-setup.exe` 并安装。
### 安装 Node.js 
打开命令行，执行：
``` bash
nvm install latest    # 安装最新版
nvm install 18        # 安装指定版本（如 18.x）
```
### 切换版本
``` bash
nvm use 18            # 切换到 18.x 版本
```
## 常见问题
- **权限问题**：如果遇到权限错误，尝试以管理员身份运行命令行。
- **环境变量未生效**：重启命令行或电脑，确保环境变量更新。
- **安装缓慢**：可以配置 npm 镜像源加速后续包下载：
``` bash
npm config set registry https://registry.npmmirror.com
```

#JavaScript #Node #Windows